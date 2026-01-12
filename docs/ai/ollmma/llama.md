基于llama.cpp 构建hugging face的模型到gguf格式。

（1）编译构建llama.cpp

* Windows：​ 推荐使用 Visual Studio 2022（Community Edition）和对应的 C++ 工作负载，或者使用 MinGW。
  * C++ CMake 工具 for Windows
  * Git for Windows
  * C++ Clang 编译器 for Windows（可选，但推荐）
  * MSBuild 支持 for LLVM 工具集（Clang）
  * choco install ninja ( Start-Process -FilePath choco -ArgumentList "install ninja -y" -Verb RunAs )
  * Start-Process -FilePath choco -ArgumentList "install gsudo -y" -Verb RunAs
* Linux：​ 通常使用 GCC 或 Clang，确保已安装构建工具（如 build-essential）。
  
```bash
mkdir build
cd build
cmake .. -G "Visual Studio 18 2026" -A x64 -DLLAMA_CURL=OFF
cmake .. -G "Visual Studio 18 2026" -A x64 -DLLAMA_CUDA=ON -DLLAMA_CURL=OFF
cmake .. -G "Ninja" -DCMAKE_BUILD_TYPE=Release -DLLAMA_CURL=OFF
cmake --build . --config Release -j 8
```

(2) 将 Hugging Face 模型转换为 GGUF 格式
uv pip install -r requirements.txt --index-url https://pypi.tuna.tsinghua.edu.cn/simple --index-strategy unsafe-best-match
uv pip install -r requirements.txt --index-url https://mirrors.aliyun.com/pypi/simple/


python convert_hf_to_gguf.py D:\documents\projects\algo-nl2sql\models\nl2sql-chinese-basic --outfile D:\documents\projects\algo-nl2sql\models\nl2sql-chinese-basic\output_model_f16.gguf --outtype f16

(3) 量化模型为 Q4_K_M 格式
./llama-quantize ./output_model_f16.gguf ./output_model_q4.gguf Q4_K_M

(4) 使用量化后的模型进行推理
./llama-cli -m ./output_model_q4.gguf -p "hello"
