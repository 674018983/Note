# BluetoothManager #

##

**解释** **：**  管理蓝牙服务的一个类。

**作用** **：** 主要用于得到一个蓝牙适配器BluetoothAdapter。

**使用小用例** **：** 

##

## 基本使用 ##

### 操作步骤: ###

- 需要权限：

		<uses-permissionandroid:name="android.permission.BLUETOOTH"/>
		<uses-permissionandroid:name="android.permission.BLUETOOTH_ADMIN"/>

- 定义了BLEDevice类，用来表示BLE设备

		public class BLEDevice {
		   private String name;
		   private String mac;
		   public BLEDevice(String name, String mac) {
		       this.name = name;
		       this.mac = mac;
		   }
		 
		   public String getName() {
		       return name;
		   }
		 
		   public void setName(String name) {
		       this.name = name;
		   }
		 
		   public String getMac() {
		       return mac;
		   }
		 
		   public void setMac(String mac) {
		       this.mac = mac;
		   }
		 
		   @Override
		   public boolean equals(Object o) {
		 
		       return !TextUtils.isEmpty(this.mac) &&!TextUtils.isEmpty(((BLEDevice)o).mac)
		                &&this.mac.equals(((BLEDevice) o).getMac());
		 
		   }
		}


- （1）获取BluetoothManager服务及BluetoothAdapter实例

		 //1.获取蓝牙管理服务及BluetoothAdapter实例
		mBluetoothManager = (BluetoothManager)getSystemService(Context.BLUETOOTH_SERVICE);
		mBluetoothAdapter = mBluetoothManager.getAdapter();   
		if (mBluetoothAdapter == null){           
			return;    
		 }

- （2）打开蓝牙（调用BluetoothAdapter的isEnabled()判断蓝牙是否打开，未打开我们可以发送一个action为BluetoothAdapter.ACTION_REQUEST_ENABLE的intent来打开蓝牙。
）

		//2. 判断蓝牙是否打开，没有打开就打开
		if (!mBluetoothAdapter.isEnabled()){
			Intent intent = newIntent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
			startActivityForResult(intent,REQUEST_ENABLE_BT);
		}

		//回调方法
		@Override
		protected void onActivityResult(int requestCode, int resultCode, Intentdata) {
		super.onActivityResult(requestCode, resultCode, data);
			if (resultCode != RESULT_OK){
				return;
			}
			if (requestCode == REQUEST_ENABLE_BT){
				Toast.makeText(this,"蓝牙已开启",Toast.LENGTH_LONG).show();
			}
		}

- （3）扫描周围的BLE蓝牙设备


		//扫描Bluetooth LE
		private void scanBleDevice(boolean enable){
			//android 5.0 以前
			if (Build.VERSION.SDK_INT < 21){
				if (enable){
					mHandler.postDelayed(new Runnable() {
						@Override
						public void run() {
						mScaning = false;
						mBluetoothAdapter.stopLeScan(mLeScanCallback);
						}
					},SCAN_SECOND);
					mScaning = true;
					mBluetoothAdapter.startLeScan(mLeScanCallback);
				} else {
					mScaning = false;
					mBluetoothAdapter.stopLeScan(mLeScanCallback);
				}
			} else {
				scanner = mBluetoothAdapter.getBluetoothLeScanner();
				scanner.startScan(mScanCallback);
					mHandler.postDelayed(new Runnable() {
						@Override
						public void run() {
						scanner.stopScan(mScanCallback);
						}
					},SCAN_SECOND);
			}
		}

	//回调方法
	

		//sacn扫描回调 5.0以上用
		private ScanCallback mScanCallback = new ScanCallback() {
		@Override
			public void onScanResult(int callbackType, ScanResult result) {
				BluetoothDevice device =result.getDevice();
				if (device != null){
					//过滤掉其他设备
					if (device.getName() != null&& device.getName().startsWith("WINPOS")){
					BLEDevice bleDevice = newBLEDevice(device.getName(),device.getAddress());
						if(!mBLEDeviceList.contains(bleDevice)){
						mBLEDeviceList.add(bleDevice);
						showBluetoothLeDevice(bleDevice);
						}
					}
				}
 
		       @Override
		       public void onBatchScanResults(List<ScanResult> results) {
		 
		           Log.d(TAG,"onBatchScanResults");
		       }
 
		       @Override
		       public void onScanFailed(int errorCode) {
		           Log.d(TAG,"onScanFailed");
		       }
		};
 
 
		//4.3以上
		private BluetoothAdapter.LeScanCallback mLeScanCallback = newBluetoothAdapter.LeScanCallback() {
			@Override
			public void onLeScan(final BluetoothDevice bluetoothDevice, int i,byte[] bytes) {
				if (bluetoothDevice != null){
					//过滤掉其他设备
					if (bluetoothDevice.getName()!= null && bluetoothDevice.getName().startsWith("WINPOS")){
					BLEDevice bleDevice = newBLEDevice(bluetoothDevice.getName(),bluetoothDevice.getAddress());
						if(!mBLEDeviceList.contains(bleDevice)){
						mBLEDeviceList.add(bleDevice);
						showBluetoothLeDevice(bleDevice);
						}
					}
				}
			}
		};


- （4）获取远程设备，连接GATT服务
##

### 实现效果/成效: ###

显示蓝牙以及连接蓝牙
	
##

### 优点 ###


### 缺点/不足 ###


##

### 更多扩展知识/具体命令详解 ###

- **BluetoothAdapter类：**代表了一个本地的蓝牙适配器。它是所有蓝牙交互的的入口点。利用它你可以发现其他蓝牙设备，查询绑定了的设备，使用已知的MAC地址实例化一个蓝牙设备和建立一个BluetoothServerSocket（作为服务器端）来监听来自其他设备的连接。

- **BluetoothDevice类：**代表了一个远端的蓝牙设备，使用它请求远端蓝牙设备连接或者获取远端蓝牙设备的名称、地址、种类和绑定状态。

- **BluetoothGatt类：**符合BLE GATT协议，封装了与其他蓝牙设备通信功能的一个类。可以通过BluetoothDevice的connectGatt(Context, boolean, BluetoothGattCallback)得到其实例。

- **GATT(Generic Attribute Profile)：**通用属性参数文件，通过BLE连接，读写属性类小数据的Profile通用规范。现在所有的BLE应用Profile都是基于GATT的。蓝牙 4.0特有。可以理解为一个规范文件。

- **ATT(Attribute Protocol) 属性协议：**GATT是基于ATTProtocol的。ATT针对BLE设备做了专门的优化，具体就是在传输过程中使用尽量少的数据。每个属性都有一个唯一的UUID，属性将以characteristics 和services的形式传输。

- **Service 服务：**Characteristic的集合。例如一个service叫做“Heart RateMonitor”，它可能包含多个Characteristics，其中可能包含一个叫做“heart rate measurement"的Characteristic。

- **Characteristic 特性：**Characteristic可以理解为一个数据类型，它包括1个value和0至多个Descriptor

- **Descriptor：**对Characteristic的描述，例如范围、计量单位等，一个Descriptor包含一个Value。



### 具体个人分析 ###

该Manager主要用于获取一个蓝牙适配器BluetoothAdapter,通过其获取所有蓝牙信息

##

### 参考文档 ###

[android BLE 编程详解](https://blog.csdn.net/qiyei2009/article/details/52026096)