# Step by Step Guide

### step 1 : create Application class and notification channel

```kotlin
class RunningApp: Application() {}
 ```

```kotlin
if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.O){  
    val notificationChannel = NotificationChannel(  
        /* id = */ "running_channel",  
        /* name = */ "Running Notification",  
        /* importance = */ NotificationManager.IMPORTANCE_HIGH  
  )  
  
    val notificationManager = getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager  
  
    notificationManager.createNotificationChannel(notificationChannel)  
}

```

Add application class in AndroidManifest .XML
```xml
<application  
  android:name=".RunningApp"
  ...
>
</application>
```

### step 2 : create Service class

```kotlin
class RunningService: Service() {  
    override fun onBind(p0: Intent?): IBinder? {  
        return null  
  }
  
  override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
	    return super.onStartCommand(intent, flags, startId)  
	}
}
```

### step 3 : initialize notification in Service class

```kotlin
val notification = NotificationCompat.Builder(this, "running_channel")  
    .setSmallIcon(R.drawable.ic_launcher_foreground)  
    .setContentTitle("This is Foreground Service")  
    .build()  
  
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {  
    startForeground(1, notification)  
}
```

### step 4 : start service via intent

```kotlin
Intent(applicationContext, RunningService::class.java).also {  
	 it.action = RunningService.Action.START.toString()  
	 startService(it)  
}
```
