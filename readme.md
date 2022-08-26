open3d code:v0.14.1
python open3d : 0.14.1

## 环境设置
设置deb
```
sudo apt install  k4a-tools
pip install open3d==0.14.1
git clone https://github.com/isl-org/Open3D.git
git checkout v0.14.1
```
将Azure-Kinect-Sensor-SDK.git 中的 ./scripts/99-k4a.rules /etc/udev/rules.d/ 
## 采集数据
- 查看相机状态

```
cd examples/python/reconstruction_system
python sensors/azure_kinect_viewer.py
```

- 查看且录制mkv数据
```
python sensors/azure_kinect_recorder.py --output ~/test.mkv #press 'space' to record
# k4arecord a.mkv  # 使用kinect官方工具录制
```

- mkv查看/mkv导出深度图和RGB图,(depth img and color img will be aligned)
```bash
python sensors/azure_kinect_mkv_reader.py --input ~/test.mkv --output ~/test_out
```

## 重建
```
python3 run_system.py --make --register --refine --integrate  ~/fu_out/config.json 
```
note if you move the test_out to other path, you need modify the config in config.json

```json
    "path_dataset": "/home/bst/test_out",
    "path_intrinsic": "/home/bst/test_out/intrinsic.json",
```
> http://www.open3d.org/docs/latest/tutorial/sensor/azure_kinect.html?highlight=kinect