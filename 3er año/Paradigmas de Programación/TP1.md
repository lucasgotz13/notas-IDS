```java
package app;
import Model.Enemigo;
import Model.EnemigoRapido;
import Model.EnemigoSimple;
import javafx.animation.AnimationTimer;
import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.scene.layout.Pane;
import javafx.scene.paint.Color;
import javafx.scene.shape.Circle;
import javafx.stage.Stage;

import java.util.ArrayList;
import java.util.List;

public class mainApp extends Application {
    private static final int WIDTH = 800;
    private static final int HEIGHT = 600;
    private static final double SPAWN_INTERVAL_SEC = 1.8;
    private static final int TOTAL_ENEMIES = 8;

    // Ruta simple de prueba (waypoints)
    private final List<Punto> ruta = List.of(
            new Punto(60, 80),
            new Punto(250, 80),
            new Punto(250, 250),
            new Punto(500, 250),
            new Punto(500, 480),
            new Punto(740, 480)
    );

    private final List<EnemyActor> enemigosActivos = new ArrayList<>();
    private int enemigosSpawneados = 0;
    private double tiempoSpawnAcumulado = 0.0;
    @Override
    public void start(Stage stage) throws Exception {
//        FXMLLoader loader = new FXMLLoader(getClass().getResource("/menu.fxml"));
//        Parent root = loader.load();
//
//        Scene scene = new Scene(root);
//        stage.setTitle("Boca Defense");
//        stage.setScene(scene);
//        stage.setResizable(false);
//        stage.show();
        Pane root = new Pane();
        root.setPrefSize(WIDTH, HEIGHT);

        for (Punto p : ruta) {
            Circle waypoint = new Circle(p.x, p.y, 4);
            root.getChildren().add(waypoint);
        }

        var scene = new Scene(root, 800, 600);
        stage.setTitle("Boca Defense");
        stage.setScene(scene);
        stage.setResizable(false);
        stage.show();


        AnimationTimer timer = new AnimationTimer() {
            private long ultimoFrameNanos = -1;
            @Override
            public void handle(long now) {
                if (ultimoFrameNanos < 0) {
                    ultimoFrameNanos = now;
                    return;
                }

                double deltaSec = (now - ultimoFrameNanos) / 1_000_000_000.0;
                ultimoFrameNanos = now;

                actualizarSpawn(deltaSec, root);
                actualizarEnemigos(deltaSec, root);
            }
        };
        timer.start();

    }

    private void actualizarSpawn(double deltaSec, Pane root) {
        if (enemigosSpawneados >= TOTAL_ENEMIES) return;

        tiempoSpawnAcumulado += deltaSec;
        if (tiempoSpawnAcumulado >= SPAWN_INTERVAL_SEC) {
            tiempoSpawnAcumulado = 0.0;
            enemigosSpawneados++;

            Punto inicio = ruta.get(0);
            Enemigo enemigoModelo = new EnemigoRapido(inicio.x, inicio.y);

            Circle vista = new Circle(inicio.x, inicio.y, 10, Color.CRIMSON);
            root.getChildren().add(vista);

            enemigosActivos.add(new EnemyActor(enemigoModelo, vista));
        }
    }

    private void actualizarEnemigos(double deltaSec, Pane root) {
        List<EnemyActor> paraRemover = new ArrayList<>();

        for (EnemyActor actor : enemigosActivos) {
            boolean llego = actor.avanzarPorRuta(ruta, deltaSec);

            // Sincroniza vista con modelo
            actor.vista.setCenterX(actor.modelo.getPosX());
            actor.vista.setCenterY(actor.modelo.getPosY());

            if (llego) {
                paraRemover.add(actor);
            }
        }

        for (EnemyActor actor : paraRemover) {
            root.getChildren().remove(actor.vista);
            enemigosActivos.remove(actor);
        }
    }

    private static class EnemyActor {
        private final Enemigo modelo;
        private final Circle vista;

        private int waypointActual = 1; // 0 es spawn
        EnemyActor(Enemigo modelo, Circle vista) {
            this.modelo = modelo;
            this.vista = vista;
        }

        // Devuelve true cuando terminó la ruta
        boolean avanzarPorRuta(List<Punto> ruta, double deltaSec) {
            if (waypointActual >= ruta.size()) {
                return true;
            }

            Punto destino = ruta.get(waypointActual);
            double dx = destino.x - modelo.getPosX();
            double dy = destino.y - modelo.getPosY();
            double dist = Math.sqrt(dx * dx + dy * dy);

            if (dist < 1.0) {
                waypointActual++;
                return waypointActual >= ruta.size();
            }

            double paso = modelo.getVelocidad() * deltaSec;
            if (paso > dist) paso = dist;

            double ux = dx / dist;
            double uy = dy / dist;

            modelo.mover(ux*paso, uy*paso);

            return false;
        }
    }

    private static class Punto {
        final double x;
        final double y;

        Punto(double x, double y) {
            this.x = x;
            this.y = y;
        }
    }
}
```

    public boolean intentarColocarTorreta(String tipo, int fila, int col) {
        // Es un slot de torreta?
        if (!matrizMapa[fila][col].equals("T")) {
            return false;
        }

        Torreta nueva = crearTorretaSegunTipo(tipo, col, fila);
        if (nueva == null) return false;

        for (Torreta t : torretasPuestas) {
            if (t.getPosX() == col && t.getPosY() == fila && !t.getNombre().equals(tipo)) {
                torretasPuestas.remove(t);
                break;
            }
        }

        // Si pasó todo, la guardamos en el Hash
        torretasPuestas.add(nueva);
        return true;
    