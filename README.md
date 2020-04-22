# Mambo-Mikrotik
Gerador de script Mikrotik em Python

while True:
  reset = input('O equipamento está resetado? s ou n: ')
  print("")
  if reset == 'n':
        print('cole no terminal do Mikrotik esse comando: system reset-configuration no-defaults=yes')
        print("")
  elif reset != 's' and reset !='n':
        print('caractere inválido, digite s ou n')
        print("")
  else:
       break
while True:
        internet = input('O equipamento possui internet? s ou  n: ')
        print("")
        if internet != 's' and internet !='n':
          print('caractere inválido, digite s ou n')
          print("")
        elif internet == 'n' :
         interface_link= input('digite a interface que receberá o link, exp: ether1, ether2: ')
         print("")
         print(f'cole no terminal do Mikrotik esse comando: /ip dhcp-client add dhcp-options=hostname,clientid disabled=no interface={interface_link}')
         print("")
         print('Para testar o link, digite no terminal do Mikrtik o comando "ping 8.8.8.8"')
         print("")
        else:
         break
while True:
        Mikrotik = input('O Mikrotik é flash? s ou n: ')
        if Mikrotik != 's' and Mikrotik !='n':
         print("")
         print('caractere inválido, digite s ou n')
         print("")
        else:
            print("")
            break
while True:
        hash = input('Digite a hash da campanha: ')
        print("")
        if len(hash) <36 or len(hash) > 36:
         print("")
         print('hash inválida')
         print("")
         continue
        else:
            print("")
        interface_captive = input('digite a interface que funcionará o captive exp: ether1, ether2, wlan1, wlan2: ')
        print("")
        if Mikrotik == 's':
         print('/interface bridge add name=bridge-hotspot')
         print('/ip address add address=10.5.50.1/24 interface=bridge-hotspot network=10.5.50.0')
         print('/ip pool add name=hs-pool-3 ranges=10.5.50.2-10.5.50.254')
         print('/ip dhcp-server add address-pool=hs-pool-3 disabled=no interface=bridge-hotspot lease-time=1h name=dhcp1')
         print('/ip dhcp-server network add address=10.5.50.0/24 comment="hotspot network" gateway=10.5.50.1')
         print('/ip dns set servers=10.5.50.1,8.8.8.8')
         print('/ip hotspot profile add hotspot-address=10.5.50.1 name=hsprof1')
         print('/ip hotspot add address-pool=hs-pool-3 disabled=no interface=bridge-hotspot name=hotspot profile=hsprof1')
         print('/ip hotspot user add name=service password=service')
         print('/ip hotspot profile set login-by=http-pap hsprof1')
         print('/ip hotspot walled-garden add action=allow dst-host="*.mambowifi.com"')
         print('/ip hotspot walled-garden ip add dst-address=52.67.12.47')
         print('/ip hotspot user profile set shared-users=unlimited default')
         print('/ip hotspot set login-timeout=30m idle-timeout=10m hotspot')
         print('/ip firewall nat add chain=srcnat src-address=10.5.50.0/24 action=masquerade')
         print(f'/interface bridge port add bridge=bridge-hotspot interface={interface_captive}')
         print('/interface wireless cap set enabled=no')
         print('/interface wireless set disabled=no mode=ap-bridge ssid="Captive Mambo" wlan1')
         print('/interface bridge port add bridge=bridge-hotspot interface=wlan1')
         print(f'/file set flash/hotspot/login.html contents="<html><head><meta http-equiv=\\"refresh\\" content=\\"0;url=http://captive.mambowifi.com/mikrotik/r/{hash}\?identity=\$(identity)&login-by=\$(login-by)&server-name=\$(server-name)&server-address=\$(server-address)&APMac=\$(APMac)&link-login-only=\$(link-login-only)&link-orig=\$(link-orig)&ip=\$(ip)&mac=\$(mac)&host-ip=\$(host-ip)&session-id=\$(session-id)&error=\$(error)\\"/><meta http-equiv=\\"pragma\\" content=\\"no-cache\\"><meta http-equiv=\\"expires\\" content=\\"0\\"></head></html>"')
         print('copie e cole o script acima no terminal')
         print("")
         finalizar = input('deseja finalizar? s ou n: ')
         if finalizar == 's':
             break
        elif Mikrotik =='n':
         print('/interface bridge add name=bridge-hotspot')
         print('/ip address add address=10.5.50.1/24 interface=bridge-hotspot network=10.5.50.0')
         print('/ip pool add name=hs-pool-3 ranges=10.5.50.2-10.5.50.254')
         print('/ip dhcp-server add address-pool=hs-pool-3 disabled=no interface=bridge-hotspot lease-time=1h name=dhcp1')
         print('/ip dhcp-server network add address=10.5.50.0/24 comment="hotspot network" gateway=10.5.50.1')
         print('/ip dns set servers=10.5.50.1,8.8.8.8')
         print('/ip hotspot profile add hotspot-address=10.5.50.1 name=hsprof1')
         print('/ip hotspot add address-pool=hs-pool-3 disabled=no interface=bridge-hotspot name=hotspot profile=hsprof1')
         print('/ip hotspot user add name=service password=service')
         print('/ip hotspot profile set login-by=http-pap hsprof1')
         print('/ip hotspot walled-garden add action=allow dst-host="*.mambowifi.com"')
         print('/ip hotspot walled-garden ip add dst-address=52.67.12.47')
         print('/ip hotspot user profile set shared-users=unlimited default')
         print('/ip hotspot set login-timeout=30m idle-timeout=10m hotspot')
         print('/ip firewall nat add chain=srcnat src-address=10.5.50.0/24 action=masquerade')
         print(f'/interface bridge port add bridge=bridge-hotspot interface={interface_captive}')
         print('/interface wireless cap set enabled=no')
         print('/interface wireless set disabled=no mode=ap-bridge ssid="Captive Mambo" wlan1')
         print('/interface bridge port add bridge=bridge-hotspot interface=wlan1')
         print(f'/file set hotspot/login.html contents="<html><head><meta http-equiv=\\"refresh\\" content=\\"0;url=http://captive.mambowifi.com/mikrotik/r/{hash}\?identity=\$(identity)&login-by=\$(login-by)&server-name=\$(server-name)&server-address=\$(server-address)&APMac=\$(APMac)&link-login-only=\$(link-login-only)&link-orig=\$(link-orig)&ip=\$(ip)&mac=\$(mac)&host-ip=\$(host-ip)&session-id=\$(session-id)&error=\$(error)\\"/><meta http-equiv=\\"pragma\\" content=\\"no-cache\\"><meta http-equiv=\\"expires\\" content=\\"0\\"></head></html>"')
         print("")
         print('copie e cole o script acima no terminal')
         print("")
         finalizar = input('deseja finalizar? s ou n: ')
         if finalizar == 's':
             break
        else:
                   break


















