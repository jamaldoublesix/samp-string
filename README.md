# samp-string
อธิบายเกี่ยวกับการวางระเบิดในสคริปในรูปแบบของ string บลาๆ *พร้อมวิธีแก้

// --! โค้ดตัวปัญหาให้สังเกตที่ string , string2 ผมไม่รู้เขาทําทําไม สามารถ fix ได้โดย -->

    case 0:
    {
        new
            count,
            var[32],
            string[512],
            string2[512];

        for (new i = 0; i != MAX_GPS; i ++) if (gpsData[i][gpsExists])
        {
            if(gpsData[i][gpsType] == 1)
            {
                format(string, sizeof(string), "%d\t%s\n", i, gpsData[i][gpsName]);
                strcat(string2, string);
                format(var, sizeof(var), "AGPSID%d", count);
                SetPVarInt(playerid, var, i);
                count++;
            }
        }
        if (!count)
        {
            SendClientMessage(playerid, COLOR_RED, "[ระบบ] {FFFFFF}เซิร์ฟเวอร์ยังไม่ได้เพิ่ม GPS");
            return 1;
        }
        format(string, sizeof(string), "ไอดี\tชื่อ\n%s", string2);
        Dialog_Show(playerid, DIALOG_AGPSPICK, DIALOG_STYLE_TABLIST_HEADERS, "[สถานที่ต่าง ๆ]", string, "เลือก", "ปิด");
    }
// --> การ fix เพื่อให้ server หน่วงน้อยหรือแตกยากแตกน้อยก็แล้วแต่การเขียนของแต่ละท่านนะครับ 55555 การหน่วงเกิดได้หลายรูปแบบ อิอิ
// * สังเกตที่ string

    case 0:
    {
        new
            count,
            var[32],
            string[512];

        strcat(string, "ไอดี\tชื่อ\n");
    
        for (new i = 0; i != MAX_GPS; i ++) if (gpsData[i][gpsExists])
        {
            if(gpsData[i][gpsType] == 1)
            {
                format(string, sizeof(string), "%s%d\t%s\n", string, i, gpsData[i][gpsName]);
                format(var, sizeof(var), "AGPSID%d", count);
                SetPVarInt(playerid, var, i);
                count++;
            }
        }
        if (!count)
        {
            SendClientMessage(playerid, COLOR_RED, "[ระบบ] {FFFFFF}เซิร์ฟเวอร์ยังไม่ได้เพิ่ม GPS");
            return 1;
        }
    
        Dialog_Show(playerid, DIALOG_AGPSPICK, DIALOG_STYLE_TABLIST_HEADERS, "[สถานที่ต่าง ๆ]", string, "เลือก", "ปิด");
    }
