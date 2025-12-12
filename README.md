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
Flash size 
<img width="1426" height="296" alt="image" src="https://github.com/user-attachments/assets/212715e0-abc7-4b44-bbb3-22a712aacfcb" />


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






