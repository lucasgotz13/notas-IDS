---
id: 1745289495-autoloading-namespaces-and-models
aliases:
  - Autoloading, Namespaces and Models
tags:
  - Laravel
  - PHP
---

# Autoloading, Namespaces and Models

## Usage of Namespaces and Models

```php
// app/models/Job.php
<?php

namespace App\Models; // This is the namespace declaration. Then we use this when we import the class in other files.

use Illuminate\Support\Arr;

class Job {
	// We declare the method for getting all the jobs
    public static function all(): array { 
        return [ /*Jobs...*/ ]
    }

    public static function find($id): array { // Method for getting job by id
        $job = Arr::first(static::all(), fn($job) => $job['id'] == $id);

        // We check if the job exists and use the abort method to throw an 404
        // error if it doesn't
        if (! job) {
            abort(404);
        }

        return $job 
    }
}
```

