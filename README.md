# SealRom
SealRom is a free and open source modification that works on various samsung devices but mostly on exynos.

TODO
* reorganize and document the source code better
  HOW TO APPLY SEALROM PATCHES

To apply services.jar patches you have to decompile framework/services.jar and apply the patch file on the source with git

Requirements to test OneUI 6 port
*Selinux Permissive kernel


  HOW TO BUILD IT ?

1. Remove fabric_crypto from bin
 
2.replace whole folder cameradata folder from stock

3.Go to etc/init/hw/init.rc  Search for '#Storage F/W update' or ''ffu' add a # in front of 'ffu' and 'ssr' which is located 1 line under

4.Go to etc/permissions replace 'camera.xml' and 'privapp-permissions-com.sec.android.app.camera.xml'  with stock

5.Go to \etc\vintf\compatibility_matrix.device.xml search for 'compatibility-matrix version' find (few lines after)  '<hal format="hidl" optional="false">' 

one line after this copy paste:

        <name>vendor.samsung_slsi.hardware.MultiFrameProcessing20</name>
        <version>1.0</version>
        <interface>
            <name>IMultiFrameProcessing20</name>
            <instance>default</instance>
        </interface>
    </hal>
    <hal format="hidl" optional="false">
	
6.search for '<name>vendor.samsung_slsi.telephony.hardware.radio</name>' find '<instance>slot1</instance>'
one line after this copy paste this:


        </interface>
    </hal>
    <hal format="hidl" optional="false">
        <name>vendor.samsung_slsi.hardware.iva</name>
        <version>1.0</version>
        <interface>
            <name>IIvaService</name>
            <instance>default</instance>
            
7.Delete 'selinux' folder from system_ext/etc

8.Go to build.prop file search for '# autogenerated by buildinfo.sh' after this line add:


ro.sf.lcd_density=420
after the line 'ro.build.id=UP1A.230905.011' add:
ro.build.display.id=SealROM V6.1 Alpha


9.Search for 'dalvik.vm.usejit=true' after this line add:


dalvik.vm.usejitprofiles=true

10.find the end of the file and add :


wlan.wfd.hdcp=disable
ro.csc.countryiso_code=DE
#TODO: maybe implement something in updater.script that sets this reading it from csc or somewhere
persist.bluetooth.a2dp_offload.disabled=true
#ro.boot.sales_code=EUX
#ro.csc.sales_code=EUX
wifi.interface=wlan0
persist.sys.no_req_encrypt=true



(The order of the lines in build prop doesn't matter)


12.Delete 
\system\preload\Facebook_stub_preload\

NOTES 

if you are planning to upload on xda a rom that uses these patches , add source link to the thread.
