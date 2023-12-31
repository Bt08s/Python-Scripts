# Wait for internet connection
```python
import socket
import time
def wait_internet_connection():
    print("Waiting for an internet connection...")
    while True:
        try:
            socket.create_connection(("8.8.8.8", 53), timeout=10)
            print("Internet connection established.")
            return True
        except:
            time.sleep(20)
```

# Enable/disable task manager
```python
# Administrator access required
import winreg
key_path = r'Software\Microsoft\Windows\CurrentVersion\Policies\System'
value_name = 'DisableTaskMgr'
value_data = 0  # 0=enable, 1=disable
key = winreg.OpenKey(winreg.HKEY_CURRENT_USER, key_path, 0, winreg.KEY_SET_VALUE)
winreg.SetValueEx(key, value_name, 0, winreg.REG_DWORD, value_data)
winreg.CloseKey(key)
```

# Check if proccess exists
```python
import psutil
def check_process_exists(process_name):
    for process in psutil.process_iter(attrs=['name']):
        if process.info['name'] == process_name:
            return True
    return False
```

# Terminate proccess
```python
import psutil
def terminate_process(process_name):
    for process in psutil.process_iter(attrs=['pid', 'name']):
        if process.info['name'] == process_name:
            pid = process.info['pid']
            try:
                p = psutil.Process(pid)
                p.terminate()
            except psutil.NoSuchProcess:
                pass
```

# "The duration of a code."
```python
import time

def format_duration(seconds):
    years, seconds = divmod(seconds, 31536000)
    days, seconds = divmod(seconds, 86400)
    hours, seconds = divmod(seconds, 3600)
    minutes, seconds = divmod(seconds, 60)

    result = ""
    if years:
        result += f"{int(years)}y "
    if days:
        result += f"{int(days)}d "
    if hours:
        result += f"{int(hours)}h "
    if minutes:
        result += f"{int(minutes)}m "
    if seconds:
        result += f"{int(seconds)}s"

    return result

start_time = time.time()

# code

end_time = time.time()
elapsed_time = end_time - start_tim
print(f"Total duration: {format_duration(elapsed_time)}")
```

# Set console title
```python
def set_title(title):
    if os.name == 'nt':
        import ctypes
        ctypes.windll.kernel32.SetConsoleTitleW(title)
    else:
        import sys
        sys.stdout.write(f"\033]0;{title}\007")
        sys.stdout.flush()
```

# Clear console
```python
def clear():
    os.system('cls' if os.name == 'nt' else 'clear')
```

# Fast open ports scan
```python
import threading
import socket
ip = 127.0.0.1
timeout = 5  # 3=fast, 5=slow

def scan_port(ip, port):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(1)

    try:
        sock.connect((ip, port))
        print(f"\033[32m[+]\033[0m {ip}:{port}")
    except socket.error:
        pass
    finally:
        sock.close()

for port in range(1, 65535):
    thread = threading.Thread(target=scan_port, args=(ip, port))
    thread.start()
```
