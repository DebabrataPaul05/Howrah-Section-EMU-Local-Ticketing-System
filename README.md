#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
typedef struct station 
{
    int prevdist, nextdist;
    int stnid, junc, line;
    char stnname[50];
    char stncode[50];
    struct station *prevstn;
    struct station *nextstn;
} stn;

typedef struct 
{
    int prevdist, nextdist;
    int stnid, junc, line;
    char stnname[50];
    char stncode[50];
} StationData;

stn *head = NULL;
StationData howrah_digha_stations[] = {
    {   0,   5, 700, 1, 7, "Howrah", "HWH" },
    {   5,   2, 701, 0, 7, "Tikiapara", "TPKR" },
    {   2,   2, 702, 0, 7, "Dasnagar", "DSNR" },
    {   2,   3, 703, 0, 7, "Ramrajatala", "RMJ" },
    {   3,   6, 704, 1, 7, "Santragachi Junction", "SRC" },
    {   6,   3, 705, 0, 7, "Maurigram", "MMG" },
    {   3,   2, 706, 0, 7, "Andul", "ADL" },
    {   2,   5, 707, 0, 7, "Sankrail", "SXL" },
    {   5,   2, 708, 0, 7, "Abada", "ABA" },
    {   2,   5, 709, 0, 7, "Nalpur", "NLP" },
    {   5,   6, 710, 0, 7, "Bauria", "BOY" },
    {   6,   5, 711, 0, 7, "Chengel", "CGL" },
    {   5,   5, 712, 0, 7, "Fuleswar", "FUL" },
    {   5,   6, 713, 0, 7, "Uluberia", "ULB" },
    {   6,   6, 714, 0, 7, "Bir Shibpur", "BSP" },
    {   6,   6, 715, 0, 7, "Kulgachia", "KGC" },
    {   6,   6, 716, 0, 7, "Bagnan", "BZN" },
    {   6,   6, 717, 0, 7, "Ghoraghata", "GHG" },
    {   6,   5, 718, 0, 7, "Deulti", "DLT" },
    {   5,   6, 719, 0, 7, "Kolaghat", "KOL" },
    {   6,   5, 720, 0, 7, "Mecheda", "MCA" },
    {   5,   3, 721, 0, 7, "Nandaigajan P.H", "NDGJ" },
    {   3,   6, 722, 0, 7, "Bhogpur", "BOP" },
    {   6,   9, 723, 0, 7, "Narayan Pakuria Murail", "NPMR" },
    {   9,   8, 724, 1, 7, "Panskura Junction", "PKU" },
    {   8,   6, 725, 0, 7, "Raghunathbari", "RGB" },
    {   6,   6, 726, 0, 7, "Rajgoda", "RJG" },
    {   6,   5, 727, 0, 7, "Saheed Matangini", "SMT" },
    {   5,   6, 728, 1, 7, "Tamluk", "TMK" },
    {   6,   3, 729, 0, 7, "Nandakumar P.H", "NDKP" },
    {   3,   3, 730, 0, 7, "Lavan Satyagrah Smarak P.H", "LSSP" },
    {   3,   3, 731, 0, 7, "Deshapran P.H", "DSHP" },
    {   3,   3, 732, 0, 7, "Henria P.H", "HNRA" },
    {   3,   3, 733, 0, 7, "Nachinda P.H", "NCHD" },
    {   3,   5, 734, 0, 7, "Kanthi", "KNTH" },
    {   5,   3, 735, 0, 7, "Sitalpur Bengal", "STPB" },
    {   3,   3, 736, 0, 7, "Sujalpur", "SJLP" },
    {   3,   3, 737, 0, 7, "Ashapurna Devi", "ASPD" },
    {   3,   3, 738, 0, 7, "Badalpur P.H", "BDLP" },
    {   3,   3, 739, 0, 7, "Ramnagar Bengal", "RMBG" },
    {   3,   3, 740, 0, 7, "Tikra P.H", "TKRP" },
    {   3,   5, 741, 1, 7, "Digha", "DG" }
};

int howrah_digha_count = sizeof(howrah_digha_stations) / sizeof(howrah_digha_stations[0]);
StationData howrah_medinipur_stations[] = {
    {   0,   3, 300, 1, 5, "Howrah", "HWH" },
    {   3,   1, 301, 0, 5, "Tikiapara", "TPKR" },
    {   1,   1, 302, 0, 5, "Dasnagar", "DSNR" },
    {   1,   2, 303, 0, 5, "Ramrajatala", "RMJ" },
    {   2,   4, 304, 1, 5, "Santragachi Junction", "SRC" },
    {   4,   2, 305, 0, 5, "Maurigram", "MMG" },
    {   2,   1, 306, 0, 5, "Andul", "ADL" },
    {   1,   3, 307, 0, 5, "Sankrail", "SXL" },
    {   3,   1, 308, 0, 5, "Abada", "ABA" },
    {   1,   3, 309, 0, 5, "Nalpur", "NLP" },
    {   3,   4, 310, 0, 5, "Bauria", "BOY" },
    {   4,   3, 311, 0, 5, "Chengel", "CGL" },
    {   3,   3, 312, 0, 5, "Fuleswar", "FUL" },
    {   3,   4, 313, 0, 5, "Uluberia", "ULB" },
    {   4,   4, 314, 0, 5, "Bir Shibpur", "BSP" },
    {   4,   4, 315, 0, 5, "Kulgachia", "KGC" },
    {   4,   4, 316, 0, 5, "Bagnan", "BZN" },
    {   4,   4, 317, 0, 5, "Ghoraghata", "GHG" },
    {   4,   3, 318, 0, 5, "Deulti", "DLT" },
    {   3,   4, 319, 0, 5, "Kolaghat", "KOL" },
    {   4,   3, 320, 0, 5, "Mecheda", "MCA" },
    {   3,   2, 321, 0, 5, "Nandaigajan P.H", "NDGJ" },
    {   2,   4, 322, 0, 5, "Bhogpur", "BOP" },
    {   4,   6, 323, 0, 5, "Narayan Pakuria Murail", "NPMR" },
    {   6,   5, 324, 1, 5, "Panskura Junction", "PKU" },
    {   5,   3, 325, 0, 5, "Khirai", "KHAI" },
    {   3,   3, 326, 0, 5, "Haur", "HAUR" },
    {   3,   3, 327, 0, 5, "Radhamohanpur", "RMP" },
    {   3,   3, 328, 0, 5, "Duan", "DUAN" },
    {   3,   3, 329, 0, 5, "Balichak", "BCK" },
    {   3,   3, 330, 0, 5, "Shyam Chak", "SMCK" },
    {   3,   3, 331, 0, 5, "Madpur", "MPD" },
    {   3,   4, 332, 1, 5, "Kharagpur Junction", "KGP" },
    {   4,   3, 333, 0, 5, "Girimaidan", "GMDN" },
    {   3,   3, 334, 0, 5, "Gokulpur", "GKL" },
    {   3,   4, 335, 0, 5, "Midnapore", "MDN" }
};
int howrah_medinipur_count = sizeof(howrah_medinipur_stations) / sizeof(howrah_medinipur_stations[0]);
StationData howrah_haldia_stations[] = {
    {   0,   3, 600, 1, 6, "Howrah", "HWH" },
    {   3,   1, 601, 0, 6, "Tikiapara", "TPKR" },
    {   1,   1, 602, 0, 6, "Dasnagar", "DSNR" },
    {   1,   2, 603, 0, 6, "Ramrajatala", "RMJ" },
    {   2,   4, 604, 1, 6, "Santragachi Junction", "SRC" },
    {   4,   2, 605, 0, 6, "Maurigram", "MMG" },
    {   2,   1, 606, 0, 6, "Andul", "ADL" },
    {   1,   3, 607, 0, 6, "Sankrail", "SXL" },
    {   3,   1, 608, 0, 6, "Abada", "ABA" },
    {   1,   3, 609, 0, 6, "Nalpur", "NLP" },
    {   3,   4, 610, 0, 6, "Bauria", "BOY" },
    {   4,   3, 611, 0, 6, "Chengel", "CGL" },
    {   3,   3, 612, 0, 6, "Fuleswar", "FUL" },
    {   3,   4, 613, 0, 6, "Uluberia", "ULB" },
    {   4,   4, 614, 0, 6, "Bir Shibpur", "BSP" },
    {   4,   4, 615, 0, 6, "Kulgachia", "KGC" },
    {   4,   4, 616, 0, 6, "Bagnan", "BZN" },
    {   4,   4, 617, 0, 6, "Ghoraghata", "GHG" },
    {   4,   3, 618, 0, 6, "Deulti", "DLT" },
    {   3,   4, 619, 0, 6, "Kolaghat", "KOL" },
    {   4,   3, 620, 0, 6, "Mecheda", "MCA" },
    {   3,   2, 621, 0, 6, "Nandaigajan P.H", "NDGJ" },
    {   2,   4, 622, 0, 6, "Bhogpur", "BOP" },
    {   4,   6, 623, 0, 6, "Narayan Pakuria Murail", "NPMR" },
    {   6,   5, 624, 1, 6, "Panskura Junction", "PKU" },
    {   5,   4, 625, 0, 6, "Raghunathbari", "RGB" },
    {   4,   4, 626, 0, 6, "Rajgoda", "RJG" },
    {   4,   3, 627, 0, 6, "Saheed Matangini", "SMG" },
    {   3,   5, 628, 0, 6, "Tamluk", "TMLK" },
    {   5,   3, 629, 0, 6, "Keshabpur", "KSBP" },
    {   3,   2, 630, 0, 6, "Satish Samanta P.H", "SSPH" },
    {   2,   3, 631, 0, 6, "Mahisadal", "MHSD" },
    {   3,   2, 632, 0, 6, "Barda", "BRDA" },
    {   2,   2, 633, 0, 6, "Basulya Sutahata", "BSTH" },
    {   2,   3, 634, 0, 6, "Durgachak", "DGCK" },
    {   3,   2, 635, 0, 6, "Durga Chak Town", "DCTN" },
    {   2,   3, 636, 1, 6, "Bardar P.H", "BDPH" },
    {   3,   0, 637, 0, 6, "Haldia", "HLDA" } 
};
int howrah_haldia_count = sizeof(howrah_haldia_stations) / sizeof(howrah_haldia_stations[0]);
StationData howrah_burdwan_stations[] = {
    {0, 5, 201, 1, 2, "Howrah", "HWH"},
	{5, 2, 202, 0, 2, "Liluah", "LLH"},
    {2, 2, 203, 0, 2, "Belur", "BEQ"},
    {2, 2, 204, 0, 2, "Bally", "BLY"},
    {2, 3, 205, 0, 2, "Uttarpara", "UPA"},
    {3, 4, 206, 0, 2, "Hind Motor", "HMZ"},
    {4, 3, 207, 0, 2, "Konnagar", "KOG"},
    {3, 3, 208, 0, 2, "Rishra", "RIS"},
    {3, 5, 209, 0, 2, "Shrirampur", "SRP"},
    {5, 7, 210, 1, 2, "Seoraphuli Junction", "SHE"},
    {0, 2, 211, 0, 2, "Baidyabati", "BBAE"},
    {2, 2, 212, 0, 2, "Bhadreswar", "BHR"},
    {2, 2, 213, 0, 2, "Mankundu", "MUU"},
    {2, 2, 214, 0, 2, "Chandannagar", "CGR"},
    {2, 2, 215, 0, 2, "Chuchura", "CNS"},
    {2, 2, 216, 0, 2, "Hooghly", "HGY"},
    {2, 4, 217, 1, 2, "Bandel Junction", "BDC"},
    {0, 4, 218, 0, 2, "Adisaptagram", "ASP"},
    {4, 5, 219, 0, 2, "Magra", "MGA"},
    {5, 3, 220, 0, 2, "Talandu", "TLD"},
    {3, 4, 221, 0, 2, "Khanyan", "KHN"},
    {4, 5, 222, 0, 2, "Pundooah", "PDA"},
    {5, 3, 223, 0, 2, "Simlagarh", "SLG"},
    {3, 3, 224, 0, 2, "Bainchigram", "BIC"},
    {3, 3, 225, 0, 2, "Bainchi", "BCI"},
    {3, 4, 226, 0, 2, "Debipur", "DBP"},
    {4, 4, 227, 0, 2, "Bagila", "BGL"},
    {4, 4, 228, 0, 2, "Memari", "MME"},
    {4, 3, 229, 0, 2, "Nimo", "NIM"},
    {3, 4, 230, 0, 2, "Rasulpur", "RSP"},
    {4, 3, 231, 0, 2, "Palsit", "PLS"},
    {3, 3, 232, 0, 2, "Saktigarh", "SKT"},
    {3, 5, 233, 0, 2, "Gangpur", "GGP"},
    {5, 0, 234, 1, 2, "Barddhaman Junction", "BWN"}
};
int howrah_burdwan_count = sizeof(howrah_burdwan_stations) / sizeof(howrah_burdwan_stations[0]);
StationData bardhaman_katwa_stations[] = {
    {   0,   3, 800, 1, 8, "Bardhaman Junction", "BWN" },
    {   3,   2, 801, 0, 8, "Kamnara", "KMRA" },
    {   2,   3, 802, 0, 8, "Khetia", "KSHT" },
    {   3,   2, 803, 0, 8, "Chamardighi", "CMDG" },
    {   2,   3, 804, 0, 8, "Karjana", "KJRA" },
    {   3,   2, 805, 0, 8, "Karjanagram", "KJRM" },
    {   2,   2, 806, 0, 8, "Amarun", "ARNB" },
    {   2,   3, 807, 0, 8, "Bhatar", "BTRH" },
    {   3,   2, 808, 0, 8, "Balgona", "BGNA" },
    {   2,   2, 809, 0, 8, "Saota", "SOF" },
    {   2,   2, 810, 0, 8, "Nigan", "NGX" },
    {   2,   1, 811, 0, 8, "Kaichar Halt", "KCY" },
    {   1,   2, 812, 0, 8, "Bankapasi", "BCF" },
    {   2,   1, 813, 0, 8, "Shrikhanda", "SIZ" },
    {   1,   1, 814, 0, 8, "Shripat Shrikhand", "SPS" },
    {   1,   0, 815, 1, 8, "Katwa Junction", "KWAE" }
};
int bardhaman_katwa_count = sizeof(bardhaman_katwa_stations) / sizeof(bardhaman_katwa_stations[0]);
StationData howrah_goghat_stations[] = {
    {0, 5, 101, 1, 1, "Howrah", "HWH"},
	{5, 2, 102, 0, 1, "Liluah", "LLH"},
	{2, 2, 103, 0, 1, "Belur", "BEQ"},
	{2, 1, 104, 0, 1, "Bally", "BLY"},
	{1, 3, 105, 0, 1, "Uttarpara", "UPA"},
	{3, 4, 106, 0, 1, "Hind Motor", "HMZ"},
	{4, 3, 107, 0, 1, "Konnagar", "KOG"},
	{3, 3, 108, 0, 1, "Rishra", "RIS"},
	{3, 5, 109, 0, 1, "Shrirampur", "SRP"},
	{5, 7, 110, 1, 1, "Seoraphuli Junction", "SHE"},
	{7, 5, 111, 0, 1, "Diara", "DEA"},
	{5, 2, 112, 0, 1, "Nasibpur", "NSF"},
	{2, 5, 113, 0, 1, "Singur", "SIU"},
	{5, 5, 114, 0, 1, "Kamarkundu", "KQLS"},
	{5, 4, 115, 0, 1, "Nalikul", "NKL"},
	{4, 4, 116, 0, 1, "Maliya Halt", "MLYA"},
	{4, 4, 117, 0, 1, "Haripal", "HPL"},
	{4, 3, 118, 0, 1, "Kaikala", "KKAE"},
	{3, 3, 119, 0, 1, "Bahir Khanda", "BAHW"},
	{3, 5, 120, 0, 1, "Loknath", "LOK"},
	{5, 10, 121, 1, 1, "Tarakeswar", "TAK"},
	{10, 4, 122, 0, 1, "Talpur Halt", "TLPH"},
	{4, 8, 123, 0, 1, "Takipur Halt", "TKPH"},
	{8, 11, 124, 0, 1, "Mayapur", "MAYP"},
	{11, 10, 125, 0, 1, "Arambagh", "AMBG"},
	{10, 0, 126, 0, 1, "Goghat", "GHT"}

};
int howrah_goghat_count = sizeof(howrah_goghat_stations) / sizeof(howrah_goghat_stations[0]);
StationData howrah_katwa_stations[] = {
	{0, 5, 501, 1, 3, "Howrah", "HWH"},
	{5, 2, 502, 0, 3, "Liluah", "LLH"},
	{2, 2, 503, 0, 3, "Belur", "BEQ"},
	{2, 2, 504, 0, 3, "Bally", "BLY"},
	{2, 3, 505, 0, 3, "Uttarpara", "UPA"},
	{3, 4, 506, 0, 3, "Hind Motor", "HMZ"},
	{4, 3, 507, 0, 3, "Konnagar", "KOG"},
	{3, 3, 508, 0, 3, "Rishra", "RIS"},
	{3, 5, 509, 0, 3, "Shrirampur", "SRP"},
	{5, 7, 510, 1, 3, "Seoraphuli Junction", "SHE"},
    {0, 2, 511, 0, 3, "Baidyabati", "BBAE"},
    {2, 2, 512, 0, 3, "Bhadreswar", "BHR"},
    {2, 2, 513, 0, 3, "Mankundu", "MUU"},
    {2, 2, 514, 0, 3, "Chandannagar", "CGR"},
    {2, 2, 515, 0, 3, "Chuchura", "CNS"},
    {2, 2, 516, 0, 3, "Hooghly", "HGY"},
    {2, 4, 517, 1, 3, "Bandel Junction", "BDC"},
    {4, 4, 518, 0, 3, "Bansberia",        "BSAE"},
    {4, 3, 519, 0, 3, "Tribeni",          "TBAE"},
    {3, 2, 520, 0, 3, "Kuntighat",        "KGT"},
    {2, 3, 521, 0, 3, "Dumurdaha",        "DDH"},
    {3, 2, 522, 0, 3, "Khamargachi",      "KMC"},
    {2, 3, 523, 0, 3, "Jirat",            "JRT"},
    {3, 2, 524, 0, 3, "Balagarh",         "BLGH"},
    {2, 3, 525, 0, 3, "Somrabar Bazaar",  "SRBZ"},
    {3, 3, 526, 0, 3, "Behula",           "BHU"},
    {3, 4, 527, 0, 3, "Guptipara",        "GTP"},
    {4, 3, 528, 0, 3, "Ambika Kalna",     "AKL"},
    {3, 4, 529, 0, 3, "Baghnapara",       "BGPA"},
    {4, 3, 530, 0, 3, "Dhatrigram",       "DTG"},
    {3, 4, 531, 0, 3, "Samudragarh",      "SMGD"},
    {4, 3, 532, 0, 3, "Kalinagar",        "KLNR"},
    {3, 3, 533, 0, 3, "Nabadwip Dham",    "NDAE"},
    {3, 4, 534, 0, 3, "Bishnupriya",      "BNPY"},
    {4, 3, 535, 0, 3, "Bhandartikuri",    "BDTK"},
    {3, 3, 536, 0, 3, "Purbasthali",      "PBST"},
    {3, 3, 537, 0, 3, "Mertala Phaleya",  "MTP"},
    {3, 3, 538, 0, 3, "Lakshmipur",       "LKPR"},
    {3, 3, 539, 0, 3, "Belerhat",         "BLHT"},
    {3, 3, 540, 0, 3, "Patuli",           "PTL"},
    {3, 3, 541, 0, 3, "Agradwip",         "AGW"},
    {3, 3, 542, 0, 3, "Sahebtala",        "SHT"},
    {3, 6, 543, 0, 3, "Dainhat",          "DNH"},
    {6, 0, 544, 1, 3, "Katwa Junction",   "KWAE"}
};
int howrah_katwa_count = sizeof(howrah_katwa_stations) / sizeof(howrah_katwa_stations[0]);
StationData bandel_naihati_stations[] = {
    {0, 3, 401, 1, 4, "Bandel Junction", "BDC"},
	{3, 2, 402, 0, 4, "Hooghly Ghat", "HYG"},
	{2, 3, 403, 0, 4, "Garifa", "GFAE"},
	{3, 0, 404, 1, 4, "Naihati Junction", "NH"}
};
int bandel_naihati_count = sizeof(bandel_naihati_stations) / sizeof(bandel_naihati_stations[0]);



stn* build_station_list(StationData *data, int count)
{
    stn *head = NULL, *prev = NULL;

    for (int i = 0; i < count; i++)
    {
        stn *newstn = (stn*) malloc(sizeof(stn));

        newstn->prevdist = data[i].prevdist;
        newstn->nextdist = data[i].nextdist;
        newstn->stnid = data[i].stnid;
        newstn->junc = data[i].junc;
        newstn->line = data[i].line;
        strcpy(newstn->stnname, data[i].stnname);
        strcpy(newstn->stncode, data[i].stncode);

        newstn->prevstn = prev;
        newstn->nextstn = NULL;

        if (prev) prev->nextstn = newstn;
        else head = newstn;

        prev = newstn;
    }
    return head;
}
StationData* find_station_by_name(const char* name)
{
    for (int i = 0; i < bardhaman_katwa_count; i++)
        if (strcasecmp(bardhaman_katwa_stations[i].stnname, name) == 0) return &bardhaman_katwa_stations[i];
    for (int i = 0; i < howrah_burdwan_count; i++)
        if (strcasecmp(howrah_burdwan_stations[i].stnname, name) == 0) return &howrah_burdwan_stations[i];
    for (int i = 0; i < howrah_goghat_count; i++)
        if (strcasecmp(howrah_goghat_stations[i].stnname, name) == 0) return &howrah_goghat_stations[i];
    for (int i = 0; i < howrah_katwa_count; i++)
        if (strcasecmp(howrah_katwa_stations[i].stnname, name) == 0) return &howrah_katwa_stations[i];
    for (int i = 0; i < howrah_medinipur_count; i++)
        if (strcasecmp(howrah_medinipur_stations[i].stnname, name) == 0) return &howrah_medinipur_stations[i];
    for (int i = 0; i < howrah_haldia_count; i++)
        if (strcasecmp(howrah_haldia_stations[i].stnname, name) == 0) return &howrah_haldia_stations[i];
    for (int i = 0; i < howrah_digha_count; i++)
        if (strcasecmp(howrah_digha_stations[i].stnname, name) == 0) return &howrah_digha_stations[i];
    for (int i = 0; i < bandel_naihati_count; i++)
        if (strcasecmp(bandel_naihati_stations[i].stnname, name) == 0) return &bandel_naihati_stations[i];
    return NULL; 
}



stn* find_station_in_list(stn *head, const char *name)
{
    while (head)
    {
        if (strcasecmp(head->stnname, name) == 0)
            return head;
        head = head->nextstn;
    }
    return NULL;
}



int compute_distance_same_line(stn *src, stn *dest)
{
    if (!src || !dest) return -1;

    stn *tmp = src;
    int dist = 0;

    // forward direction
    while (tmp && tmp != dest)
    {
        dist += tmp->nextdist;
        tmp = tmp->nextstn;
    }
    if (tmp == dest) return dist;

    // backward direction
    tmp = src;
    dist = 0;

    while (tmp && tmp != dest)
    {
        dist += tmp->prevdist;
        tmp = tmp->prevstn;
    }
    if (tmp == dest) return dist;

    return -1;
}

//========================================================
//          AUTO INTERLINE CONNECTIVITY (JUNCTION ROUTING)
//========================================================

int compute_interline_distance(StationData *src, StationData *dest)
{
    if (src->line == dest->line)
        return -1; // same line handled earlier

    // List of major junctions that exist in multiple lines
    const char *junctions[] = {
        "Howrah", "Santragachi Junction",
        "Bandel Junction", "Seoraphuli Junction",
        "Panskura Junction", "Bardhaman Junction",
        "Katwa Junction"
    };

    int jcount = 7;
    int best_dist = 999999;

    for (int i = 0; i < jcount; i++)
    {
        StationData *j = find_station_by_name(junctions[i]);
        if (!j) continue;

        // ---------- Route: SRC ? Junction ----------
        stn *lineA = NULL;
        int Aline = src->line;

        switch (Aline)
        {
            case 1: lineA = build_station_list(howrah_goghat_stations, howrah_goghat_count); break;
            case 2: lineA = build_station_list(howrah_burdwan_stations, howrah_burdwan_count); break;
            case 3: lineA = build_station_list(howrah_katwa_stations, howrah_katwa_count); break;
            case 4: lineA = build_station_list(bandel_naihati_stations, bandel_naihati_count); break;
            case 5: lineA = build_station_list(howrah_medinipur_stations, howrah_medinipur_count); break;
            case 6: lineA = build_station_list(howrah_haldia_stations, howrah_haldia_count); break;
            case 7: lineA = build_station_list(howrah_digha_stations, howrah_digha_count); break;
            case 8: lineA = build_station_list(bardhaman_katwa_stations, bardhaman_katwa_count); break;
        }

        stn *snode = find_station_in_list(lineA, src->stnname);
        stn *jnode = find_station_in_list(lineA, j->stnname);
        if (!snode || !jnode) continue;

        int dist1 = compute_distance_same_line(snode, jnode);
        if (dist1 < 0) continue;

        // ---------- Route: Junction ? DEST ----------
        stn *lineB = NULL;
        int Bline = dest->line;

        switch (Bline)
        {
            case 1: lineB = build_station_list(howrah_goghat_stations, howrah_goghat_count); break;
            case 2: lineB = build_station_list(howrah_burdwan_stations, howrah_burdwan_count); break;
            case 3: lineB = build_station_list(howrah_katwa_stations, howrah_katwa_count); break;
            case 4: lineB = build_station_list(bandel_naihati_stations, bandel_naihati_count); break;
            case 5: lineB = build_station_list(howrah_medinipur_stations, howrah_medinipur_count); break;
            case 6: lineB = build_station_list(howrah_haldia_stations, howrah_haldia_count); break;
            case 7: lineB = build_station_list(howrah_digha_stations, howrah_digha_count); break;
            case 8: lineB = build_station_list(bardhaman_katwa_stations, bardhaman_katwa_count); break;
        }

        stn *jnode2 = find_station_in_list(lineB, j->stnname);
        stn *dnode = find_station_in_list(lineB, dest->stnname);
        if (!jnode2 || !dnode) continue;

        int dist2 = compute_distance_same_line(jnode2, dnode);
        if (dist2 < 0) continue;

        if (dist1 + dist2 < best_dist)
            best_dist = dist1 + dist2;
    }

    return (best_dist == 999999) ? -1 : best_dist;
}
int ticketcalculate(int dist, int r)
{
    int price;
    if (dist <= 20) price = 5;
    else if (dist>20 && dist<=44) price = 10;
    else if (dist>44 && dist <= 60) price = 15;
    else if (dist>60 && dist <= 75) price = 20;
    else if (dist>75 && dist <= 90) price = 25;
    else if (dist>90 && dist <= 110) price = 30;
    else if (dist>110 && dist <= 130) price = 40;
    else if (dist>130 && dist <= 150) price = 50;
    else if (dist>150 && dist <= 180) price = 65;
    else if (dist>180 && dist <= 200) price = 90;
    else if (dist>200 && dist <= 220) price = 100;
    else if (dist>220 && dist <= 240) price = 120;
    else if (dist>240 && dist <= 300) price = 150;
    else price=200;

    if (r == 1) price *= 2;
    return price;
}
void generate_ticket_id(char *out)
{
    srand(time(NULL));
    long t = time(NULL);
    int r = rand() % 90000 + 10000;

    sprintf(out, "TKT-%d-%ld", r, t);
}
void generateticket(const char *source, const char *destination,
                    int dist, int price, int rtype)
{
    char tid[50];
    generate_ticket_id(tid);

    printf("\n----------------------------------------\n");
    printf("        INDIAN RAILWAY TICKET\n");
    printf("----------------------------------------\n");
    printf("Ticket ID    : %s\n", tid);
    printf("From Station : %s\n", source);
    printf("To Station   : %s\n", destination);
    printf("Distance     : %d km\n", dist);
    printf("Trip Type    : %s\n", (rtype ? "Round Trip" : "One Way"));
    printf("Ticket Price : Rs. %d\n", price);
    printf("----------------------------------------\n");
    printf("Thank you for travelling with us!\n");
    printf("----------------------------------------\n\n");
}
int main()
{
    int more;
    do {
        char src[50], dest[50];
        int r;

        printf("Enter Source Station: ");
        fgets(src, 50, stdin); src[strcspn(src, "\n")] = 0;

        printf("Enter Destination Station: ");
        fgets(dest, 50, stdin); dest[strcspn(dest, "\n")] = 0;

        printf("Enter 1 for round trip, else 0: ");
        scanf("%d", &r); getchar();

        StationData *s = find_station_by_name(src);
        StationData *d = find_station_by_name(dest);

        if (!s || !d) {
            printf("Invalid station entered.\n");
            continue;
        }

        int total_dist = -1;

        if (s->line == d->line)
        {
            // Same line case
            int sl = s->line;
            int dl = d->line;
            int c = (dl > sl) ? dl : sl;

            switch (c) 
			{
                case 1:
                    head = build_station_list(howrah_goghat_stations, howrah_goghat_count);
                    break;
                case 2:
                    head = build_station_list(howrah_burdwan_stations, howrah_burdwan_count);
                    break;
                case 3:
                    head = build_station_list(howrah_katwa_stations, howrah_katwa_count);
                    break;
                case 4:
                    head = build_station_list(bandel_naihati_stations, bandel_naihati_count);
                    break;
                case 5:
                	head = build_station_list(howrah_medinipur_stations, howrah_medinipur_count);
                    break;
                case 6:
                	head = build_station_list(howrah_haldia_stations, howrah_haldia_count);
                    break;
                case 7:
                	head = build_station_list(howrah_digha_stations, howrah_digha_count);
                    break;
                case 8:
                	head = build_station_list(bardhaman_katwa_stations, bardhaman_katwa_count);
                    break;
                default:
                    printf("Sorry... Direct ticket of such route can't be generated.\n");
                    head = NULL;
                    break;
            }

            stn *sn = find_station_in_list(head, src);
            stn *dn = find_station_in_list(head, dest);

            total_dist = compute_distance_same_line(sn, dn);
        }
        else
        {
            // Interline connectivity
            total_dist = compute_interline_distance(s, d);
        }

        if (total_dist < 0)
        {
            printf("Sorry... No valid route found.\n");
        }
        else
        {
            if (r == 1) total_dist *= 2;

            int price = ticketcalculate(total_dist, 0);
            generateticket(src, dest, total_dist, price, r);
        }

        printf("Generate more tickets? Enter 1: ");
        scanf("%d", &more);
        getchar();
    } while (more == 1);

    return 0;
}

