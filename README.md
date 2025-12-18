# Esp32FlashEncryption
<img width="842" height="473" alt="image" src="https://github.com/user-attachments/assets/8ccb495d-a73e-4c07-b8dc-0d2b9d813307" />
<img width="851" height="254" alt="image" src="https://github.com/user-attachments/assets/099f5f44-b1fe-4801-bc45-59294ca4812c" />
<img width="871" height="438" alt="image" src="https://github.com/user-attachments/assets/0a123f21-21d7-487a-ad66-eb215c4ac19b" />
<img width="852" height="601" alt="image" src="https://github.com/user-attachments/assets/f375de0a-b15f-4689-a486-dc09df66da86" />
<img width="850" height="680" alt="image" src="https://github.com/user-attachments/assets/f80d1bf3-1216-4d0c-ae34-8b5db9893339" />

# EspTool
pip install esptool
<img width="1517" height="748" alt="image" src="https://github.com/user-attachments/assets/eb51c8e6-5836-4891-a6c9-aebc9134ee27" />
    Đưa ESP32 vào chế độ download (boot mode) 
    python -m esptool --port COM4 read-flash 0 0x400000 flash_contents.bin
<img width="852" height="258" alt="image" src="https://github.com/user-attachments/assets/d76c8f12-d627-4eba-8ae6-c14daeb3c962" />

use IDF terminal in visual studio code 
python -m esptool --port COM5 read_flash 0 0x400000 flash_contents.bin
<img width="938" height="308" alt="image" src="https://github.com/user-attachments/assets/011e48ad-9942-46ed-94c7-56e5c6dfcd1f" />


# IDF Extention and arduino core
<img width="862" height="703" alt="image" src="https://github.com/user-attachments/assets/c6be9444-1b5a-4f97-817a-36791d3bfc4a" />
<img width="1210" height="644" alt="image" src="https://github.com/user-attachments/assets/43c16a41-9367-48e0-9d3c-7d84d529ef66" />
<img width="1396" height="320" alt="image" src="https://github.com/user-attachments/assets/6ad86044-2455-4d20-ab08-b67fc94aaffa" />

<img width="854" height="823" alt="image" src="https://github.com/user-attachments/assets/0e8cc330-3641-4468-a048-89d82fdb2240" />


# Bootloader Size Issue
<img width="849" height="544" alt="image" src="https://github.com/user-attachments/assets/75d8f751-a053-4c51-8ab5-045c325c141a" />

# IDF build

Full Clean: idf.py fullclean \
<img width="753" height="117" alt="image" src="https://github.com/user-attachments/assets/67ffa942-fbfb-4c8f-987e-bfb77abb9f72" />

Menuconfig: idf.py menuconfig \
<img width="873" height="347" alt="image" src="https://github.com/user-attachments/assets/5d674ea8-8a0b-4b91-b79c-2f11bf67d56e" />

Set Target Chip \
<img width="1021" height="342" alt="image" src="https://github.com/user-attachments/assets/9adafeb9-6cea-48a9-bfe4-387233149a62" />
<img width="709" height="114" alt="image" src="https://github.com/user-attachments/assets/d94caa7c-f5cb-44ab-8c02-8e53aae0b91b" />
<img width="685" height="350" alt="image" src="https://github.com/user-attachments/assets/b5566aa7-656d-4b21-8f31-e22b28d33e10" />

Earse Flash in esp32 \
esptool.py --chip esp32 erase_flash
<img width="678" height="237" alt="image" src="https://github.com/user-attachments/assets/bef7b74d-5f89-4058-9ccf-4aa82d549353" />



IDF flash: idf.py flash
<img width="1243" height="415" alt="image" src="https://github.com/user-attachments/assets/e7c704fd-4cf8-42fa-8ee0-9c70f68d051b" />






# Name, Type, SubType, Offset, Size, Flags
nvs, data, nvs, 0x9000, 0x6000,  # 24 KB
otadata, data, ota, 0xF000, 0x2000,  # 8 KB
app0, app, factory, 0x10000, 0xD0000,  # 832 KB
# You can add more partitions below as needed

# IDF menuconfig
1. Flash size 
CONFIG_ESPTOOLPY_FLASHSIZE="4MB"
<img width="1426" height="296" alt="image" src="https://github.com/user-attachments/assets/212715e0-abc7-4b44-bbb3-22a712aacfcb" />
2. Flash encryption
<img width="562" height="227" alt="image" src="https://github.com/user-attachments/assets/27bc1e52-f0ba-428b-b969-dadb3213466b" />
3. Partition Table
<img width="1476" height="238" alt="image" src="https://github.com/user-attachments/assets/914aeb12-59c6-4e9e-9ed1-a51acfbef3e4" />



# Custom partittion csv file to idf project.
1. Update partitions.csv from arduino ide
   <img width="1282" height="444" alt="image" src="https://github.com/user-attachments/assets/a2a9675e-73b2-4285-876a-fef29acb5aa7" />

2. Place your partitions.csv file in your project directory
   Typically, put it in the root of your project or in a dedicated folder, e.g., components/partition/.

# Perform flashing with esp32 bin file
1. Create key file:
   python -m espsecure.generate_flash_encryption_key flash_enc_key.bin
2. Encrypt bin file from arduino ide (ie output.bin )
   python -m espsecure.encrypt_flash --keyfile=flash_enc_key.bin --output=output_encrypted.bin output.bin
3. Earse flash before flashing
   esptool.py --chip esp32 --port COM3 erase_flash
4. Flash encripted bin file to esp32
   esptool.py --chip esp32 --port COM3 --baud 115200 write_flash 0x10000 output_encrypted.bin

The offset value is got from partittion.csv file.
<img width="855" height="457" alt="image" src="https://github.com/user-attachments/assets/ecd193d0-a891-4913-90cb-d6b98b993f46" />

# Guidle 
1. Official Document
   https://docs.espressif.com/projects/esp-idf/en/release-v4.0/security/flash-encryption.html#:~:text=When%20flash%20encryption%20is%20enabled%2C%20physical%20readout,the%20data%20in%20place%20on%20first%20boot.
# Step from user
https://github.com/espressif/arduino-esp32/issues/5645#issuecomment-961191953
1. Using a simple project from ESP-IDF (for example Hello-World)
2. adding Arduino Components as following:
https://docs.espressif.com/projects/arduino-esp32/en/latest/esp-idf_component.html
3. adding suitable sdkconfig from Arduino folder to the project folder (from ..\components\arduino\tools\sdk\esp32 for ESP32)
4. adding customized partition.csv as follow to the project:
Name, Type, SubType, Offset, Size, Flags
nvs, data, nvs, 0x9000, 0x5000,
otadata, data, ota, 0xe000, 0x2000,
app0, app, ota_0, 0x10000, 0x140000,
nvs_key, data, nvs_keys,0x285000,0x1000,
spiffs, data, spiffs, 0x290000,0x170000,

<img width="827" height="242" alt="image" src="https://github.com/user-attachments/assets/f338714c-ae96-4459-b84c-13d647eefc90" />

6. enabling the encryption and customized partition table by
idf.py menuconfig
7. building the projekt by:
idf.py build
8. copying the built partition-table.bin (from ..\build\partition_table) , the built bootloader.bin (from ..\build\bootloader) and ota_data_initial.bin (from ..\build) to the esptool folder (..\esp-idf\components\esptool_py\esptool)
9. convert the Arduino sketch to binary by: Arduino IDE-> Sketch-> Export compiled binary (rename it as main.bin)
10. copying the main.bin to the esptool folder
11.  creating own key
espsecure.py generate_flash_encryption_key my_flash_encryption_key.bin
12.  write the key in the module
espefuse.py --port PORT burn_key flash_encryption my_flash_encryption_key.bin
13. write all the files to the module:
esptool.py -p PORT -b 921600 --before default_reset --after no_reset --chip esp32 write_flash --flash_mode dio --flash_size detect --flash_freq 40m 0x1000 bootloader.bin 0x8000 partition-table.bin 0xe000 ota_data_initial.bin 0x10000 main.bin 0x290000 spiffs.bin
14. it will encrypt the flash and restart
to rewrite the module for development, use the development mode in step 5 and encrypt the main.bin file:
espsecure.py encrypt_flash_data --keyfile my_flash_encryption_key.bin --address 0x10000 --output main_en.bin main.bin
and write this part only:
esptool.py -p PORT -b 921600 write_flash --flash_mode dio 0x10000 main_en.bin

# My Steps
Component Manager
<img width="1226" height="676" alt="image" src="https://github.com/user-attachments/assets/27606192-51a5-4941-b877-ccac8992c67f" />
<img width="1167" height="667" alt="image" src="https://github.com/user-attachments/assets/3660d104-e1de-40d4-bcb0-9c78215b62cc" />
<img width="1493" height="369" alt="image" src="https://github.com/user-attachments/assets/e926e484-b604-4d7e-8f88-f0ee4f1989c5" />


1. Open Visual Studio Code 
   <img width="1443" height="615" alt="image" src="https://github.com/user-attachments/assets/265cc8cf-9c91-4a15-b9ba-00da6659b08a" />
2. Choice "hello_world"
   <img width="1709" height="532" alt="image" src="https://github.com/user-attachments/assets/6fb3840b-a6aa-4552-bed8-5da2315b82d1" />
3. Add Arduino component
   idf.py add-dependency "espressif/arduino-esp32" 
   <img width="1477" height="673" alt="image" src="https://github.com/user-attachments/assets/fc813967-8024-4632-9902-6f02388bf013" />
   <img width="1182" height="499" alt="image" src="https://github.com/user-attachments/assets/bdc0f84f-bb68-48d5-a71c-5cd4652ae68a" />

4. Run menuconfig by command "idf.py menuconfig" \
   idf.py create-project-from-example "espressif/arduino-esp32^3.3.3:hello_world" \
   cd hello_world \

# Deactivate Flash Encryption
Read Summary \
espefuse.py -p COM5 summary \

esptool.py -p COM5 erase_flash --force \

idf.py efuse-write-protect DISABLE_DL_ENCRYPT \
<img width="1134" height="479" alt="image" src="https://github.com/user-attachments/assets/2f2dda89-3a31-4c0f-9e86-31ea5fa19ce7" />

Reset board and force Flash \ 
idf.py flash -p COM5 --force

# Partition Table
<img width="690" height="505" alt="image" src="https://github.com/user-attachments/assets/df2a061b-6e27-4658-984b-6f5dbf180b8b" />

# AI Steps
<img width="689" height="508" alt="image" src="https://github.com/user-attachments/assets/5f0dbd22-4e2d-44fc-91a0-4c8e6520f158" />  

    espsecure.py generate_flash_encryption_key flash_encryption_key.bin 
    
    
<img width="676" height="442" alt="image" src="https://github.com/user-attachments/assets/5c5cd38f-ff84-4daa-9374-8cc994c42d42" />
<img width="672" height="555" alt="image" src="https://github.com/user-attachments/assets/27814a9a-24b1-4785-85c2-cbd0072fa085" />

    espsecure.py encrypt_flash_data --keyfile flash_encryption_key.bin --address 0x1000 --output bootloader_encrypted.bin bootloader.bin \
    espsecure.py encrypt_flash_data --keyfile flash_encryption_key.bin --address 0x8000 --output partitions_encrypted.bin partitions.bin \
    espsecure.py encrypt_flash_data --keyfile flash_encryption_key.bin --address 0x10000 --output sketch_encrypted.bin your_sketch.ino.bin \
    
<img width="675" height="397" alt="image" src="https://github.com/user-attachments/assets/48ec8c6c-68d6-4d12-a02e-1d35dfd9d0b2" />



