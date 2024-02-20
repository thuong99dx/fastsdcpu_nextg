Find what you need faster … 
Home is your new landing page and surfaces your most relevant files and folders
ReadMe.md

#Fastsd CPU-Openvino  
##Hướng dẫn cài đặt
#1. FastSD CPU on Linux
- Cài đặt Python >=3.8.

- Clone repo: $ git clone https://github.com/rupeshs/fastsdcpu.git
 hoặc https://github.com/thuong99dx/fastsdcpu_nextg.git
- Cách 1:
  - Vào terminal, đi đến thư mục fastsdcpu

  - Thực thi các lệnh command sau để cài đặt

      $ chmod +x install.sh
    
      $ ./install.sh

  - Chạy chương trình trên Desktop GUI (liên quan đến thư viện pygqt gui của python)  
  $ ./start.sh

  - Chạy trên trình duyệt Web UI
  $ ./start-webui.sh
- Cách 2:
  - Tạo môi trường ảo:   
    - $ sudo apt install -y python3-venv
    - $ python3 -m venv name_env
    - $ source name_env/bin/activate
  - Cài đặt thư viện:
    - $ pip install diffusers==0.23.0 transformers==4.35.0 accelerate==0.23.0 Pillow==9.4.0 pydantic==2.4.2 pyyaml==6.0.1 gradio==3.39.0 peft==0.6.1 openvino
  - Chạy chương trình:
    - $ python src/app.py -r --share  
    Truy cập vào đường dẫn: http://127.0.0.1:7860
    
Ngoài ra trong quá trình cài đặt có thể yều cầu phát sinh thêm các thư viện khác, theo dõi log để thực hiện thêm đáp ứng chương trình.