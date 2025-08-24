# python package example

use uv init

```sh
uv init.
```

sync package

```sh
uv sync
```

add require

```sh
uv add build
```

# build

## use `setuptools` as backend

```sh
python -m build
# or
uv build
```

## use `hatching` as backend

https://hatch.pypa.io/latest/

`pyproject.toml` 中添加

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```

然后

```sh
python -m build
# or
uv build
```

## 调整代码目录格式

```txt
src/`和项目同名文件夹`
```

然后在 `pyproject.toml` 中添加如下代码告诉 `hatching` 如何找到对应目录

```toml
# 应对 hatching 打包可能出现的错误
# 这样别人安装的话, 会在它的安装目录下 package_example 使用这个名字
# src/... 是 hatch 默认的打包结构, 所以下面2行是可以注释掉的
[tool.hatch.build.targets.wheel]
packages = ["src/package_example"]
```

然后

```sh
python -m build
# or
uv build
```

# 写代码过程中需要执行的操作

把自己的代码安装到自己的环境中，防止因为路径问题找不到代码文件（主要是源代码中使用绝对导入路径可能导致的问题）

```sh
pip install -v -e .
```

如果使用 `uv` 管理项目，可以使用如下代码测试代码是否正常

```sh
uv run src/xxx.py 
uv run src/package_example/__init__.py
```

