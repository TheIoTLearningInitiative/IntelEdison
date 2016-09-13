# WiFi

## Fixed IP

```sh
$ vim /etc/wpa_supplicant/wpa_cli-actions.sh
```

```
if [ "$CMD" = "CONNECTED" ]; then
    kill_daemon udhcpc /var/run/udhcpc-$IFNAME.pid
#   udhcpc -i $IFNAME -p /var/run/udhcpc-$IFNAME.pid -S
    ifconfig $IFNAME 192.168.1.171 netmask 255.255.255.0
    route add default gw 192.168.1.1
fi
```

## Password Lenght

> ... I am asked for a 5 or 13 character network password, but my network's password is 10 characters long ... [Edison WiFi setup - password must be either 5 or 13 characters](https://communities.intel.com/thread/59888?start=0&tstart=0)

```sh
--- configure_edison.orig
+++ configure_edison
@@ -60,6 +60,15 @@
   wep_key0="%s"
}
'''  
+  WEP_26HEX =  '''
+network={
+  ssid="%s"
+  %s
+  key_mgmt=NONE
+  group=WEP104 WEP40
+  wep_key0=%s
+}
+'''
   WPAPSK =  '''
network={
   ssid="%s"
@@ -359,10 +368,13 @@
       return wpa_templates.OPEN % (ssid, "scan_ssid=1")
     elif security == 1:
       password = ''
-      while len(password) != 5 and len(password) != 13:
-        print "Password must be either 5 or 13 characters."
+      while len(password) != 5 and len(password) != 13 and len(password) != 26:
+        print "Password must be either 5 or 13 ascii characters or 26 hex."
         password = getNetworkPassword()
-      return wpa_templates.WEP % (ssid, "scan_ssid=1", password)
+        if len(password) == 26:
+          return wpa_templates.WEP_26HEX % (ssid, "scan_ssid=1", password)
+        else:
+          return wpa_templates.WEP % (ssid, "scan_ssid=1", password)
     elif security == 2:
       password = ''
       while len(password) < 8 or len(password) > 63:
@@ -384,10 +396,13 @@
     return wpa_templates.OPEN % (ssid, "")
   elif network_map[ssid] == "WEP":
     password = ''
-    while len(password) != 5 and len(password) != 13:
-        print "Password must be either 5 or 13 characters."
+    while len(password) != 5 and len(password) != 13 and len(password) != 26:
+        print "Password must be either 5 or 13 ascii characters or 26 hex."
         password = getNetworkPassword()
-    return wpa_templates.WEP % (ssid, "", password)
+        if len(password) == 26:
+          return wpa_templates.WEP_26HEX % (ssid, "", password)
+        else:
+          return wpa_templates.WEP % (ssid, "", password)
   elif network_map[ssid] == "WPA-PSK":
     password = ''
     while len(password) < 8 or len(password) > 63:
@@ -409,10 +424,13 @@
     return wpa_templates.OPEN % (ssid, "scan_ssid=1")
   elif protocol == "WEP":
     password = changewifi[2]
-    if len(password) != 5 and len(password) != 13:
-        print "Password must be either 5 or 13 characters."
+    if len(password) != 5 and len(password) != 13 and len(password) != 26:
+        print "Password must be either 5 or 13 ascii characters or 26 hex."
         return None
-    return wpa_templates.WEP % (ssid, "scan_ssid=1", password)
+    if len(password) == 26:
+      return wpa_templates.WEP_26HEX % (ssid, "scan_ssid=1", password)
+    else:
+      return wpa_templates.WEP % (ssid, "scan_ssid=1", password)
   elif protocol == "WPA-PSK":
     password = changewifi[2]
     if len(password) < 8 or len(password) > 63:
```
