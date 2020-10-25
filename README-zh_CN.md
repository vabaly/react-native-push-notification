```ts
// import PushNotificationIOS from "@react-native-community/push-notification-ios";
import PushNotification from 'react-native-push-notification';

PushNotification.configure({
  // Token 生成的时候被触发调用
  onRegister (token) {
    console.log('onRegister', token);
  },

  // 当接收到或打开远程通知，或者打开一个本地通知时被触发调用
  onNotification (notification) {
    console.log('onNotification', notification);

    // 处理 notification

    // 这是干什么的？
    // notification.finish(PushNotificationIOS.FetchResult.NoData);
  },

  // Android 平台下，当通知注册的一个动作被触发时调用，
  // 如果该函数返回 false，则仅打开 App，如果该函数返回 true，则调用上面的 onNotification 方法
  onAction (notification) {
    console.log('onAction', notification);

    // 处理 notification
  },

  // 当用户无法注册远程通知时调用。 通常在 APNS 出现问题或设备是模拟器时发生
  onRegistrationError (error) {
    console.log('onRegistrationError', error)
  },

  // 权限，默认是 all
  permissions: {
    // 弹窗
    alert: true,
    // 右上角的数字
    badge: true,
    // 声音
    sound: true,
  },

  // 初始通知是否应自动弹出，默认是 true
  popInitialNotification: true,

  /**
   *（可选）默认值：true
   * - 指定是否要请求权限（ios）和令牌（android和ios），
   * - 如果不是，则必须稍后调用PushNotificationsHandler.requestPermissions（）
   * - 如果您不使用远程通知或未安装Firebase，请使用以下命令：
   *   requestPermissions：Platform.OS ==='ios'
   */
  requestPermissions: true,
})
```

```ts
useEffect(() => {
    fetch('https://pc.suishenyun.net/peacock/api/h5/festival')
      .then(response => {
        return response.json()
      })
      .then(response => {
        console.log('response', response)
      })
    PushNotification.localNotificationSchedule({
      messageId: 'workday',
      message: 'hello, world',
      date: new Date(Date.now() + 2 * 1000),
    })
    PushNotification.localNotificationSchedule({
      messageId: 'workday',
      message: 'hello, world',
      date: new Date(Date.now() + 5 * 1000),
    })
    PushNotification.localNotificationSchedule({
      messageId: 'workday',
      message: 'hello, world',
      date: new Date(Date.now() + 60 * 1000),
    })
    PushNotification.localNotificationSchedule({
      messageId: 'workday',
      message: 'hello, world',
      date: new Date(Date.now() + 120 * 1000),
    })
  }, [])

  const handlePress = () => {
    PushNotification.getDeliveredNotifications((notifications) => {
      console.log('getDeliveredNotifications', notifications)
    })
    PushNotification.getScheduledLocalNotifications((notifications) => {
      console.log('getScheduledLocalNotifications', notifications)
    })
  }
```