API details refer to index.html in path documnent_english

Note that DO NOT OPEN SERIAL COM TWICE IN ONE APP OR OTHER PROCESS.YOU NEED CLOSE COM AFTER APP EXIT

Simple step:

1.In android studio project,import board_comm-release.aar as below:

  implementation(name: 'board_comm-release', ext: 'aar')

2.Open serial com task in your app code.  
  DoorAccessCommManager.getInstance().openComm("/dev/ttyS3",9600,seriallistener );

3.Set mcu message callback,implement interfaces you need.
  DoorAccessCommManager.getInstance().setOnBoardCommRequest(mcuCallback);

4.Send unlock cmd to mcu automatically
  
  unlockCardId = CRC16M.getSendBuf("0000000000000000");
  DoorAccessCommManager.getInstance().sendOpenCommand(unlockCardId,DoorAccessCommManager.ACCESS_MODE_MANUAL);

5.For MCU watchdog, you need open MCU watchdog function manually by sending sendWatchOgCommand£¨pls note param£©,Watchdog can monitor android sys and your app running state. for example, if your app crashed or anr or android sys crash , then MCU could not receive sendWatchOgCommand in 2mins £¬MCU will restart android sys.

  unlockCardId = CRC16M.getSendBuf("0000000000000000");
  //open or feed MCU watchdog
  DoorAccessCommManager.getInstance().sendWatchogCommand(unlockCardId,2);

5.Close serial com while app exit.

  DoorAccessCommManager.getInstance().closeComm();



Led light operation£º
1.GpioController.turnOnLed()
2.GpioController.turnOffLed()


