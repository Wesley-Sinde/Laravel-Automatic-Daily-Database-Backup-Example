# Laravel-Automatic-Daily-Database-Backup-Example.

#Laravel  Cron Job Task Scheduling Tutorial
Laravel cron job task scheduling example; Through this tutorial, i am going to show you how to create and setup cron job task scheduling in laravel  apps.


# Laravel 9Cron Job Task Scheduling Tutorial
Use the below given steps to create cron job and scheduling task in laravel 9 apps:
```php
Step 1: Create Cron Job Command Class
Step 2: Implement Logic In Cronjob Class
Step 3: Register Cron job Command
Step 4: Run Scheduler Command For Test
Step 5: Laravel Set CronJob Live Server
```
# Step 1: Create Cron Job Command Class

Run the following command on command prompt to navigate in laravel app directory:
```php
cd /blog
```
Run the following command on command prompt to create LogCron job class:

```php
php artisan make:command LogCron --command=log:cron
```
# Step 2: Implement Logic In Cronjob Class
@ Go to app/Console/Commands/ directory and open LogCron.php file. And add the following code into it:
```php
<?php
   
namespace App\Console\Commands;
   
use Illuminate\Console\Command;
   
class LogCron extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'log:cron';
    
    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'Command description';
    
    /**
     * Create a new command instance.
     *
     * @return void
     */
    public function __construct()
    {
        parent::__construct();
    }
    
    /**
     * Execute the console command.
     *
     * @return mixed
     */
    public function handle()
    {
        \Log::info("Cron is working fine!");
     
        /*
           Write your database logic we bellow:
           Item::create(['name'=>'hello new']);
        */
    }
}
```
# Step 3: Register Cron job Command
Register the above created cron job class in kernel.php file.

@ Go to app/Console directory and open Kernel.php. Then register cron job command like following:


```php
<?php
   
namespace App\Console;
    
use Illuminate\Console\Scheduling\Schedule;
use Illuminate\Foundation\Console\Kernel as ConsoleKernel;
    
class Kernel extends ConsoleKernel
{
    /**
     * The Artisan commands provided by your application.
     *
     * @var array
     */
    protected $commands = [
        Commands\LogCron::class,
    ];
     
    /**
     * Define the application's command schedule.
     *
     * @param  \Illuminate\Console\Scheduling\Schedule  $schedule
     * @return void
     */
    protected function schedule(Schedule $schedule)
    {
        $schedule->command('log:cron')
                 ->everyMinute();
    }
     
    /**
     * Register the commands for the application.
     *
     * @return void
     */
    protected function commands()
    {
        $this->load(__DIR__.'/Commands');
     
        require base_path('routes/console.php');
    }
}
```
In Kernel.php file you can schedule the task to be done when it will be the command execute(run).

List of methods for scheduler:


|Duration	| Run the task  |
| --- | --- |
|->everyMinute();	| Run the task every minute |
|->everyFiveMinutes();		| Run the task every five minutes |
| ->everyFifteenMinutes();	| 	Run the task every fifteen minutes |
|->everyTenMinutes();		| Run the task every ten minutes|
|->everyFifteenMinutes();	| 	Run the task every fifteen minutes|
|->everyThirtyMinutes();	| 	Run the task every thirty minutes|
|->hourly();	| 	Run the task every hour|
|->hourlyAt(17);	| 	Run the task every hour at 17 mins past the hour|
|->daily();		| Run the task every day at midnight|
|->dailyAt(’13:00′);		| Run the task every day at 13:00|
|->twiceDaily(1, 13);		| Run the task daily at 1:00 & 13:00|
|->weekly();		| Run the task every week|
|->weeklyOn(1, ‘8:00’);		| Run the task every week on Tuesday at 8:00|
|->monthly();		| Run the task every month|
|->monthlyOn(4, ’15:00′);		| Run the task every month on the 4th at 15:00|
|->quarterly();		| Run the task every quarter|
|->yearly();		| Run the task every year|
|->timezone(‘America/New_York’);		| Set the timezone|

# Step 4: Run Scheduler Command For Test
Run the following command on command prompt to run scheduler:

```php
php artisan schedule:run
```
# Step 5: Laravel Set CronJob on live server
To schedule the task on live server use the below command :
```php

* * * * * php /path/to/artisan schedule:run 1>> /dev/null 2>&1

OR

* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1
```
# Conclusion
Laravel 9 Cron Job task scheduling tutorial; You have successfully created cronjob and also how to run scheduler in laravel  apps.
