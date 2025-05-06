---
id: 1744687512-view-data-and-route-wildcards
aliases:
  - View data and Route Wildcards
tags:
  - Laravel
  - PHP
---

# View data and Route Wildcards

#### Last class -> How to use props

```php
@props(['name' => 'Lucas'])
<p>My name is {{ $name }}</p>
```

#### You can pass data to a view() in the second parameter of the function

```php
<?php
Route::get('/jobs', function () {
    return view('jobs', [
        'name' => 'Lucas',
        'jobs' => [
                [
                    'id' => 1,
                    'title' => 'Software Engineer',
                    'description' => 'Develop and maintain software applications.',
                ],
                [
                    'id' => 2,
                    'title' => 'Data Analyst',
                    'description' => 'Analyze and interpret complex data sets.',
                ],
            ]
        ],
    ]);
});
```

- To render the data in the view:

```php
<h1>Title: {{ $job['title'] }}</h1>
<p>Description: {{ $job['description'] }}</p>
```

#### How to make a dynamic route (for example, to have a view for each job in the jobs array):
```php
<?php
Route::get('/jobs/{id}', function ($id) {
    $jobs = [
        [
            'id' => 1,
            'title' => 'Software Engineer',
            'description' => 'Develop and maintain software applications.',
        ],
        [
            'id' => 2,
            'title' => 'Data Analyst',
            'description' => 'Analyze and interpret complex data sets.',
        ],
    ];

    $job = Arr::first($jobs, fn($job) => $job['id'] == $id); // We use the Arr function from Laravel


    return view('job', ['job' => $job);
});
```
