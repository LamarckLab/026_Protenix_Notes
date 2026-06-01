## Lamarck &nbsp; &nbsp; &nbsp; 2026-06-01
#### 该文档使用 conda & pip 部署 Protenix
---

## 01  创建 conda 环境
```bash
conda create -n lmk_Protenix python=3.11 -y --solver=classic
conda activate lmk_Protenix
```

## 02  安装 Protenix
> 
```bash
# 把三个基础组件更新到最新版本
python -m pip install --upgrade pip setuptools wheel
# 从 PyPI 官方源下载 Protenix
python -m pip install --upgrade protenix --index-url https://pypi.org/simple
# 首次执行 protenix 会用 ninja 即时编译自定义 CUDA 算子，编译结果会缓存，之后启动秒进
protenix --help
# 检查已安装的 Protenix 版本
python -m pip show protenix | grep Version
```

## 03  配置权重 / 缓存目录
Protenix 用环境变量 `PROTENIX_ROOT_DIR` 控制下载根目录，激活环境时自动生效，权重与缓存统一放 **/data/lmk/protenix_downloads**
```bash
mkdir -p /data/lmk/protenix_downloads
```
```bash
mkdir -p $CONDA_PREFIX/etc/conda/activate.d
cat > $CONDA_PREFIX/etc/conda/activate.d/protenix_env.sh <<'EOF'
export PROTENIX_ROOT_DIR=/data/lmk/protenix_downloads
EOF
source $CONDA_PREFIX/etc/conda/activate.d/protenix_env.sh
```
验证环境变量
```bash
echo $PROTENIX_ROOT_DIR
```

## 04  Protenix 输入输出目录
**236 机子路径**
> 输入目录：/data/lmk/protenix_inputs
> 输出目录：/data/lmk/protenix_outputs
```bash
mkdir -p /data/lmk/protenix_inputs
mkdir -p /data/lmk/protenix_outputs
```


##### [Protenix 官方仓库](https://github.com/bytedance/Protenix)
