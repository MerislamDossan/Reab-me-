import telnetlib
import time

host = '172.16.128.1'
user = 'user1'
password = 'user@123'
UserPrompt = '>'
ConfigPrompt = ']'

tn = telnetlib.Telnet(host)

tn.read_until(b'Username:')
tn.write(user.encode('ascii') + b'\n')
tn.read_until(b'Password:')
tn.write(password.encode('ascii') + b'\n')

print('Connection to ' + host + ' is Successful')

UserMode = tn.read_until(UserPrompt.encode('ascii'))
print(UserMode.decode('ascii'))

tn.write(b'system-view \n')
ConfigMode = tn.read_until(ConfigPrompt.encode('ascii'))
print(ConfigMode.decode('ascii'))

tn.write(b'interface LoopBack 0 \n')
ConfigMode = tn.read_until(ConfigPrompt.encode('ascii'))
print(ConfigMode.decode('ascii'))

tn.write(b'ip address 50.0.1.1 24 \n')
ConfigMode = tn.read_until(ConfigPrompt.encode('ascii'))
print(ConfigMode.decode('ascii'))

tn.write(b'display ip interface brief \n')
ConfigMode = tn.read_until(ConfigPrompt.encode('ascii'))
print(ConfigMode.decode('ascii'))

tn.close()
