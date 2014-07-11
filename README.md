Configuración en Asterisk
(lab-niv1 → Asterisk 11.10.2)

#sip-red.conf
[sipp]
username=sipp
secret=f8c1f71d847827309cdd6a944edea998
type=friend
deny=0.0.0.0/0
permit=192.168.0.0/255.255.0.0
language=es
record_out=Never
record_in=Never
qualify=no
port=5060
pickupgroup=0
callgroup=0
nat=no
host=dynamic
dtmfmode=rfc2833
context=sipp
canreinvite=no
call-limit=3
accountcode=2004
setvar=__PBX=0
setvar=__DstPBX=0
setvar=__VMCONTEXT=default
setvar=__ECID=2004
callerid="" <2004>

[sipp_2]
username=sipp_2
secret=f8c1f71d847827309cdd6a944edea998
type=friend
context=sipp
host=192.168.5.115
deny=0.0.0.0/0
permit=192.168.0.0/255.255.0.0
language=es
record_out=Never
record_in=Never
qualify=no
port=5060
pickupgroup=0
callgroup=0
nat=no
host=dynamic
dtmfmode=rfc2833
context=sipp    
canreinvite=no
call-limit=3
accountcode=2005
setvar=__PBX=0
setvar=__DstPBX=0
setvar=__VMCONTEXT=default
setvar=__ECID=2005
callerid="" <2005>

#/etc/asterisk/extensions_custom.conf 
[sipp]
exten => 2004,1,Macro(dial-exten,SIP/sipp,sipp,es)
exten => 2005,1,Macro(dial-exten,SIP/sipp_2,sipp,es)



Configuración UAC

acruz-pc$ sudo ./sipp -sf Reg_inv_test.xml -s 2005 -inf Param_file_sequential.txt -d 20000 192.168.5.6:6960 -l 1 -r 1 -i 192.168.111.207

Configuración UAS

#sipp -sn uas -p 5060 -i 192.168.5.115 -mi 192.168.5.115

