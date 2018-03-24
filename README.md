
# WeatherPy
GWU Data Analytics Bootcamp Homework 6

### Observations

* Temperature maximizes as latitude approaches 0
* Because latitude is 0 at the Equator, this means that temperature is typically highest at or near the Equator
* There does not seem to be a correlation between latitude and cloudiness, humidity, or wind speed


```python
# Read in Dependencies

import random
from citipy import citipy
import pandas as pd
import openweathermapy.core as owm
from config import api_key
import matplotlib.pyplot as plt
```

### Generate Cities List


```python
# Set possible ranges for latitude (x) and longitude (y)

xRange = (-55, 80)
yRange = (-180, 180)

# Create a place to put latitude-longitude pairs

randpoints = []

# Create a list of 2,000 latitude-longitude pairs

while len(randpoints) < 2000:
    x = random.randrange(*xRange)
    y = random.randrange(*yRange)
    if (x, y) not in randpoints:
        randpoints.append((x,y))

# Create a place to hold city data
        
cities = []

# Create a list of City objects from latitude-longitude pairs

for coordinate_pair in randpoints:
    lat, lon = coordinate_pair
    if citipy.nearest_city(lat, lon) not in cities:
        cities.append(citipy.nearest_city(lat, lon))

# Create a place to hold city names
        
names = []

# Create a list of city names from City objects

for city in cities:
    if city.city_name not in names:
        names.append(city.city_name)
```

### Perform API Calls


```python
# Create base settings for API calls

settings = {"units": "imperial", "appid": api_key}

# Create places to hold data from iterations and initiate iteration counter

name_list = []
latitude = []
temperature = []
humidity = []
cloudiness = []
wind_speed = []
i = 0

# Run API calls and collect data

for name in names:
    try:
        current_weather = owm.get_current(name, **settings)
        name_list.append(current_weather['name'])
        latitude.append(current_weather['coord']['lat'])
        temperature.append(current_weather['main']['temp'])
        humidity.append(current_weather['main']['humidity'])
        cloudiness.append(current_weather['clouds']['all'])
        wind_speed.append(current_weather['wind']['speed'])
        i = i + 1
        print(f"Record {i} for {current_weather['name']} processed!")
    except: 
        pass
```

    Record 1 for Boden processed!
    Record 2 for Naze processed!
    Record 3 for Maningrida processed!
    Record 4 for Qaqortoq processed!
    Record 5 for Srednekolymsk processed!
    Record 6 for College processed!
    Record 7 for Aklavik processed!
    Record 8 for Guozhen processed!
    Record 9 for Rikitea processed!
    Record 10 for Port Elizabeth processed!
    Record 11 for Yarensk processed!
    Record 12 for Hasaki processed!
    Record 13 for Mataura processed!
    Record 14 for Kattivakkam processed!
    Record 15 for Faanui processed!
    Record 16 for Narsaq processed!
    Record 17 for Butaritari processed!
    Record 18 for Nabire processed!
    Record 19 for Nosy Varika processed!
    Record 20 for Alofi processed!
    Record 21 for Acajutla processed!
    Record 22 for Chuy processed!
    Record 23 for Cidreira processed!
    Record 24 for Provideniya processed!
    Record 25 for Makkaveyevo processed!
    Record 26 for Port Blair processed!
    Record 27 for Bethel processed!
    Record 28 for Wattegama processed!
    Record 29 for Klaksvik processed!
    Record 30 for Guerrero Negro processed!
    Record 31 for Basco processed!
    Record 32 for Mahibadhoo processed!
    Record 33 for Kota Kinabalu processed!
    Record 34 for Hokitika processed!
    Record 35 for Hobart processed!
    Record 36 for Umm Lajj processed!
    Record 37 for Arraial do Cabo processed!
    Record 38 for Jamestown processed!
    Record 39 for Alberton processed!
    Record 40 for Formosa processed!
    Record 41 for Batemans Bay processed!
    Record 42 for Kapaa processed!
    Record 43 for Puerto Ayora processed!
    Record 44 for Rawson processed!
    Record 45 for Geraldton processed!
    Record 46 for Baruun-Urt processed!
    Record 47 for Souillac processed!
    Record 48 for Ouegoa processed!
    Record 49 for Atuona processed!
    Record 50 for Qaanaaq processed!
    Record 51 for Miquelon processed!
    Record 52 for Pangkalanbuun processed!
    Record 53 for Najran processed!
    Record 54 for Dandong processed!
    Record 55 for East London processed!
    Record 56 for Ternate processed!
    Record 57 for Dalaba processed!
    Record 58 for Ilulissat processed!
    Record 59 for Avarua processed!
    Record 60 for Kazuno processed!
    Record 61 for Busselton processed!
    Record 62 for Bongandanga processed!
    Record 63 for Cabanbanan processed!
    Record 64 for Fort Morgan processed!
    Record 65 for Morro Bay processed!
    Record 66 for Norman Wells processed!
    Record 67 for Nhulunbuy processed!
    Record 68 for Albany processed!
    Record 69 for Sarangani processed!
    Record 70 for Leverkusen processed!
    Record 71 for Kikuchi processed!
    Record 72 for Vaini processed!
    Record 73 for Shingu processed!
    Record 74 for Nikolskoye processed!
    Record 75 for Mount Gambier processed!
    Record 76 for Saint George processed!
    Record 77 for Kavieng processed!
    Record 78 for Victoria processed!
    Record 79 for Cockburn Town processed!
    Record 80 for Sulangan processed!
    Record 81 for Okhotsk processed!
    Record 82 for Cape Town processed!
    Record 83 for Kieta processed!
    Record 84 for Riberalta processed!
    Record 85 for Kouroussa processed!
    Record 86 for Port Hardy processed!
    Record 87 for Mar del Plata processed!
    Record 88 for Lavrentiya processed!
    Record 89 for Iqaluit processed!
    Record 90 for Clyde River processed!
    Record 91 for Bayan processed!
    Record 92 for Emerald processed!
    Record 93 for Presidente Medici processed!
    Record 94 for Castro processed!
    Record 95 for Lagoa processed!
    Record 96 for Sao Filipe processed!
    Record 97 for Chalmette processed!
    Record 98 for Piacabucu processed!
    Record 99 for Hilo processed!
    Record 100 for Georgetown processed!
    Record 101 for Manta processed!
    Record 102 for Amos processed!
    Record 103 for Salalah processed!
    Record 104 for Port Moresby processed!
    Record 105 for Juchitlan processed!
    Record 106 for Cherskiy processed!
    Record 107 for Catuday processed!
    Record 108 for Gorontalo processed!
    Record 109 for Kodiak processed!
    Record 110 for Denizli processed!
    Record 111 for The Valley processed!
    Record 112 for Igarka processed!
    Record 113 for Tuktoyaktuk processed!
    Record 114 for Lompoc processed!
    Record 115 for Gordeyevka processed!
    Record 116 for Monrovia processed!
    Record 117 for Flinders processed!
    Record 118 for Syedove processed!
    Record 119 for Kyzyl-Mazhalyk processed!
    Record 120 for Ushuaia processed!
    Record 121 for Yerofey Pavlovich processed!
    Record 122 for Lixourion processed!
    Record 123 for Nanortalik processed!
    Record 124 for Dingle processed!
    Record 125 for Saskylakh processed!
    Record 126 for Barrow processed!
    Record 127 for Atar processed!
    Record 128 for Bambous Virieux processed!
    Record 129 for Punta Arenas processed!
    Record 130 for Emilio Carranza processed!
    Record 131 for Novyy Nekouz processed!
    Record 132 for Waingapu processed!
    Record 133 for Dikson processed!
    Record 134 for Goderich processed!
    Record 135 for Te Anau processed!
    Record 136 for Limon processed!
    Record 137 for Maceio processed!
    Record 138 for Pacific Grove processed!
    Record 139 for Los Alamos processed!
    Record 140 for Ayagoz processed!
    Record 141 for Christchurch processed!
    Record 142 for Esperance processed!
    Record 143 for Thompson processed!
    Record 144 for Lishui processed!
    Record 145 for Coffs Harbour processed!
    Record 146 for Honiara processed!
    Record 147 for Copiapo processed!
    Record 148 for Sangar processed!
    Record 149 for Novyy Urengoy processed!
    Record 150 for Maragogi processed!
    Record 151 for Eenhana processed!
    Record 152 for Belmonte processed!
    Record 153 for Sitka processed!
    Record 154 for Mandalgovi processed!
    Record 155 for Sabya processed!
    Record 156 for Bafoulabe processed!
    Record 157 for Saint-Augustin processed!
    Record 158 for Jacareacanga processed!
    Record 159 for Saldanha processed!
    Record 160 for Chishtian Mandi processed!
    Record 161 for Champerico processed!
    Record 162 for Caravelas processed!
    Record 163 for Pueblo processed!
    Record 164 for Constitucion processed!
    Record 165 for Tigil processed!
    Record 166 for Wilmington processed!
    Record 167 for Sambava processed!
    Record 168 for Martapura processed!
    Record 169 for Yellowknife processed!
    Record 170 for Hermanus processed!
    Record 171 for Tazovskiy processed!
    Record 172 for New Norfolk processed!
    Record 173 for Torbay processed!
    Record 174 for Buraydah processed!
    Record 175 for Satka processed!
    Record 176 for Tasiilaq processed!
    Record 177 for Airai processed!
    Record 178 for Lasa processed!
    Record 179 for Turochak processed!
    Record 180 for Broome processed!
    Record 181 for Pangnirtung processed!
    Record 182 for Katsuura processed!
    Record 183 for Port Macquarie processed!
    Record 184 for Berndorf processed!
    Record 185 for Prince George processed!
    Record 186 for Alyangula processed!
    Record 187 for Oktyabrskiy processed!
    Record 188 for Vila Velha processed!
    Record 189 for Sorong processed!
    Record 190 for Tapiramuta processed!
    Record 191 for Springbok processed!
    Record 192 for Awjilah processed!
    Record 193 for Saurimo processed!
    Record 194 for Dudinka processed!
    Record 195 for Labuhan processed!
    Record 196 for Kutum processed!
    Record 197 for Caconda processed!
    Record 198 for Hofn processed!
    Record 199 for Mafra processed!
    Record 200 for Longyearbyen processed!
    Record 201 for Bilma processed!
    Record 202 for Salinas processed!
    Record 203 for Naryan-Mar processed!
    Record 204 for Upington processed!
    Record 205 for Maniitsoq processed!
    Record 206 for Chinchani processed!
    Record 207 for Tilichiki processed!
    Record 208 for Mitu processed!
    Record 209 for Ushtobe processed!
    Record 210 for Ponta do Sol processed!
    Record 211 for Belaya Gora processed!
    Record 212 for Cabo San Lucas processed!
    Record 213 for Tezu processed!
    Record 214 for Port Lincoln processed!
    Record 215 for Port Alfred processed!
    Record 216 for Soe processed!
    Record 217 for Along processed!
    Record 218 for Evreux processed!
    Record 219 for Coos Bay processed!
    Record 220 for Marica processed!
    Record 221 for Sola processed!
    Record 222 for Uruzgan processed!
    Record 223 for Adrar processed!
    Record 224 for Luanda processed!
    Record 225 for Dalby processed!
    Record 226 for Puerto Escondido processed!
    Record 227 for Almaznyy processed!
    Record 228 for Dukat processed!
    Record 229 for Kangasala processed!
    Record 230 for Paris processed!
    Record 231 for Vigrestad processed!
    Record 232 for Haines Junction processed!
    Record 233 for Talnakh processed!
    Record 234 for Nizhniy Kuranakh processed!
    Record 235 for Fernley processed!
    Record 236 for Odessa processed!
    Record 237 for Vostok processed!
    Record 238 for Palmer processed!
    Record 239 for Aljezur processed!
    Record 240 for Hambantota processed!
    Record 241 for Edd processed!
    Record 242 for Manaia processed!
    Record 243 for Bubaque processed!
    Record 244 for Mount Isa processed!
    Record 245 for Hithadhoo processed!
    Record 246 for Petropavlovsk-Kamchatskiy processed!
    Record 247 for Buchanan processed!
    Record 248 for Horsham processed!
    Record 249 for Lebu processed!
    Record 250 for Lobito processed!
    Record 251 for Abaza processed!
    Record 252 for Shasta Lake processed!
    Record 253 for Pimentel processed!
    Record 254 for La Paz processed!
    Record 255 for Vestmannaeyjar processed!
    Record 256 for Paamiut processed!
    Record 257 for Beterou processed!
    Record 258 for Mayo processed!
    Record 259 for Chokurdakh processed!
    Record 260 for Mehamn processed!
    Record 261 for Bandarbeyla processed!
    Record 262 for Lakes Entrance processed!
    Record 263 for Sinegorye processed!
    Record 264 for Upernavik processed!
    Record 265 for Mathbaria processed!
    Record 266 for Tulum processed!
    Record 267 for San Patricio processed!
    Record 268 for Piedecuesta processed!
    Record 269 for Mustasaari processed!
    Record 270 for Governador Valadares processed!
    Record 271 for Akdepe processed!
    Record 272 for Brownwood processed!
    Record 273 for Sinnamary processed!
    Record 274 for Panaba processed!
    Record 275 for Ambilobe processed!
    Record 276 for Kapit processed!
    Record 277 for Ugoofaaru processed!
    Record 278 for Rock Hill processed!
    Record 279 for Khani processed!
    Record 280 for Yulara processed!
    Record 281 for Semenyih processed!
    Record 282 for Severo-Kurilsk processed!
    Record 283 for Tuatapere processed!
    Record 284 for Codrington processed!
    Record 285 for Coahuayana processed!
    Record 286 for Kyshtovka processed!
    Record 287 for Bicester processed!
    Record 288 for Tashtyp processed!
    Record 289 for Mae Sai processed!
    Record 290 for Progreso processed!
    Record 291 for Necochea processed!
    Record 292 for Muros processed!
    Record 293 for Myaundzha processed!
    Record 294 for Verkhoyansk processed!
    Record 295 for Sioux Lookout processed!
    Record 296 for Koutsouras processed!
    Record 297 for Hamilton processed!
    Record 298 for Pangai processed!
    Record 299 for Yilan processed!
    Record 300 for Taoudenni processed!
    Record 301 for Kahului processed!
    Record 302 for Kerrobert processed!
    Record 303 for Skibbereen processed!
    Record 304 for Soyo processed!
    Record 305 for Sabha processed!
    Record 306 for Lesogorsk processed!
    Record 307 for Khatanga processed!
    Record 308 for Severnoye processed!
    Record 309 for Tiarei processed!
    Record 310 for Yenotayevka processed!
    Record 311 for Palana processed!
    Record 312 for Isangel processed!
    Record 313 for Bredasdorp processed!
    Record 314 for Jalu processed!
    Record 315 for Ukiah processed!
    Record 316 for Itarema processed!
    Record 317 for Olinda processed!
    Record 318 for Fairbanks processed!
    Record 319 for Mangrol processed!
    Record 320 for Saint-Philippe processed!
    Record 321 for Zvenigovo processed!
    Record 322 for Madison processed!
    Record 323 for Okato processed!
    Record 324 for Puri processed!
    Record 325 for Coquimbo processed!
    Record 326 for Iwanai processed!
    Record 327 for Conceicao do Araguaia processed!
    Record 328 for Inhambane processed!
    Record 329 for Pevek processed!
    Record 330 for Taunton processed!
    Record 331 for Nioaque processed!
    Record 332 for Bathsheba processed!
    Record 333 for Charlestown processed!
    Record 334 for Vallenar processed!
    Record 335 for Koeru processed!
    Record 336 for Taiobeiras processed!
    Record 337 for Moose Factory processed!
    Record 338 for Peniche processed!
    Record 339 for Carnarvon processed!
    Record 340 for Nishihara processed!
    Record 341 for Ballina processed!
    Record 342 for Nalut processed!
    Record 343 for Lanivtsi processed!
    Record 344 for Muroto processed!
    Record 345 for State College processed!
    Record 346 for San Jose processed!
    Record 347 for Kostomuksha processed!
    Record 348 for Nador processed!
    Record 349 for Komsomolskiy processed!
    Record 350 for Lata processed!
    Record 351 for Amazar processed!
    Record 352 for Umm Kaddadah processed!
    Record 353 for La Ronge processed!
    Record 354 for Porto Novo processed!
    Record 355 for Podyuga processed!
    Record 356 for Ossora processed!
    Record 357 for Canakkale processed!
    Record 358 for Vysokogornyy processed!
    Record 359 for San Quintin processed!
    Record 360 for Sayyan processed!
    Record 361 for Rome processed!
    Record 362 for Kaitangata processed!
    Record 363 for Charagua processed!
    Record 364 for Usinsk processed!
    Record 365 for Conceicao da Barra processed!
    Record 366 for Mangai processed!
    Record 367 for Manicore processed!
    Record 368 for Barcelos processed!
    Record 369 for Voznesenye processed!
    Record 370 for Gedo processed!
    Record 371 for Abnub processed!
    Record 372 for Cachoeira do Sul processed!
    Record 373 for Tatarsk processed!
    Record 374 for Dolores processed!
    Record 375 for Vodnyy processed!
    Record 376 for Poum processed!
    Record 377 for Binzhou processed!
    Record 378 for Cenade processed!
    Record 379 for Ranau processed!
    Record 380 for Vuktyl processed!
    Record 381 for Port Hedland processed!
    Record 382 for Izhma processed!
    Record 383 for Calama processed!
    Record 384 for Kavaratti processed!
    Record 385 for Teguise processed!
    Record 386 for Benguela processed!
    Record 387 for Marquette processed!
    Record 388 for Khasan processed!
    Record 389 for Doka processed!
    Record 390 for Ayan processed!
    Record 391 for Tonantins processed!
    Record 392 for Baghdad processed!
    Record 393 for Penzance processed!
    Record 394 for Yertsevo processed!
    Record 395 for Alekseyevka processed!
    Record 396 for Boende processed!
    Record 397 for Qeshm processed!
    Record 398 for General Roca processed!
    Record 399 for Khorixas processed!
    Record 400 for Lillooet processed!
    Record 401 for Atambua processed!
    Record 402 for Goundam processed!
    Record 403 for Sisimiut processed!
    Record 404 for Santa Rosa processed!
    Record 405 for Nicolas Bravo processed!
    Record 406 for Melville processed!
    Record 407 for Pondicherry processed!
    Record 408 for Camacari processed!
    Record 409 for Hervey Bay processed!
    Record 410 for Rafraf processed!
    Record 411 for Mwene-Ditu processed!
    Record 412 for Kuito processed!
    Record 413 for Acapulco processed!
    Record 414 for Belyy Yar processed!
    Record 415 for Iquique processed!
    Record 416 for Carmarthen processed!
    Record 417 for Limbang processed!
    Record 418 for Mahalapye processed!
    Record 419 for Lajas processed!
    Record 420 for Luderitz processed!
    Record 421 for Antalaha processed!
    Record 422 for Tautira processed!
    Record 423 for Merauke processed!
    Record 424 for Bilibino processed!
    Record 425 for Beloha processed!
    Record 426 for Tres Arroyos processed!
    Record 427 for San Carlos del Zulia processed!
    Record 428 for Arman processed!
    Record 429 for Karasuk processed!
    Record 430 for Balud processed!
    Record 431 for Hami processed!
    Record 432 for Miracema do Tocantins processed!
    Record 433 for Kidal processed!
    Record 434 for Macklin processed!
    Record 435 for Wewak processed!
    Record 436 for Mawlaik processed!
    Record 437 for Puerto del Rosario processed!
    Record 438 for San Carlos de Bariloche processed!
    Record 439 for Havelock processed!
    Record 440 for Quatre Cocos processed!
    Record 441 for Panama City processed!
    Record 442 for Brae processed!
    Record 443 for Luwuk processed!
    Record 444 for Umba processed!
    Record 445 for Namibe processed!
    Record 446 for Nyamuswa processed!
    Record 447 for The Pas processed!
    Record 448 for High Rock processed!
    Record 449 for Port Hawkesbury processed!
    Record 450 for Hailin processed!
    Record 451 for Lazaro Cardenas processed!
    Record 452 for Sinegorskiy processed!
    Record 453 for Kormilovka processed!
    Record 454 for Vakhrushev processed!
    Record 455 for Flin Flon processed!
    Record 456 for Havre-Saint-Pierre processed!
    Record 457 for Ancud processed!
    Record 458 for Ostrovnoy processed!
    Record 459 for Grindavik processed!
    Record 460 for Amurrio processed!
    Record 461 for Porto Velho processed!
    Record 462 for Korem processed!
    Record 463 for Tivaouane processed!
    Record 464 for Moron processed!
    Record 465 for Cayenne processed!
    Record 466 for Hagere Hiywet processed!
    Record 467 for Oistins processed!
    Record 468 for Munai processed!
    Record 469 for Kadyy processed!
    Record 470 for San Cristobal processed!
    Record 471 for West Wendover processed!
    Record 472 for Mahebourg processed!
    Record 473 for Isiro processed!
    Record 474 for Kodinsk processed!
    Record 475 for Oyama processed!
    Record 476 for Rapid Valley processed!
    Record 477 for Nkhotakota processed!
    Record 478 for Mazatlan processed!
    Record 479 for Ciudad Guayana processed!
    Record 480 for Sorland processed!
    Record 481 for Mantua processed!
    Record 482 for Cap Malheureux processed!
    Record 483 for Simao processed!
    Record 484 for Quang Ngai processed!
    Record 485 for Itupiranga processed!
    Record 486 for Yenagoa processed!
    Record 487 for Nome processed!
    Record 488 for Saint-Pierre processed!
    Record 489 for Padang processed!
    Record 490 for Haripur processed!
    Record 491 for Dejen processed!
    Record 492 for Craig processed!
    Record 493 for Onega processed!
    Record 494 for Aransas Pass processed!
    Record 495 for Gambela processed!
    Record 496 for Norsup processed!
    Record 497 for Llaillay processed!
    Record 498 for Riyadh processed!
    Record 499 for Zhigalovo processed!
    Record 500 for Kruisfontein processed!
    Record 501 for Calgary processed!
    Record 502 for Huron processed!
    Record 503 for Coroata processed!
    Record 504 for Bulgan processed!
    Record 505 for Namatanai processed!
    Record 506 for Gat processed!
    Record 507 for Lewisporte processed!
    Record 508 for Dumabato processed!
    Record 509 for Asadabad processed!
    Record 510 for Manokwari processed!
    Record 511 for Muriti processed!
    Record 512 for Prince Rupert processed!
    Record 513 for Baijiantan processed!
    Record 514 for Zhezkazgan processed!
    Record 515 for Sundargarh processed!
    Record 516 for Winslow processed!
    Record 517 for Albion processed!
    Record 518 for Marzuq processed!
    Record 519 for Hanmer Springs processed!
    Record 520 for Ust-Maya processed!
    Record 521 for Smithers processed!
    Record 522 for Itoman processed!
    Record 523 for Nago processed!
    Record 524 for Jinotega processed!
    Record 525 for Fortuna processed!
    Record 526 for Kargasok processed!
    Record 527 for Mwinilunga processed!
    Record 528 for Bonavista processed!
    Record 529 for Kem processed!
    Record 530 for Alugan processed!
    Record 531 for Hammerfest processed!
    Record 532 for Neuquen processed!
    Record 533 for Yarmouth processed!
    Record 534 for South Yuba City processed!
    Record 535 for Shenjiamen processed!
    Record 536 for Pierre processed!
    Record 537 for Salekhard processed!
    Record 538 for Vila Franca do Campo processed!
    Record 539 for Erzin processed!
    Record 540 for Mincivan processed!
    Record 541 for Margate processed!
    Record 542 for Vao processed!
    Record 543 for Port-Gentil processed!
    Record 544 for Tiksi processed!
    Record 545 for Sagna processed!
    Record 546 for Nara processed!
    Record 547 for Kalmunai processed!
    Record 548 for Whitianga processed!
    Record 549 for Pemberton processed!
    Record 550 for Ulladulla processed!
    Record 551 for Shirokiy processed!
    Record 552 for Waipawa processed!
    Record 553 for Manzhouli processed!
    Record 554 for Yumen processed!
    Record 555 for Salym processed!
    Record 556 for Urucara processed!
    Record 557 for Husavik processed!
    Record 558 for Yerbogachen processed!
    Record 559 for Tevaitoa processed!
    Record 560 for Fort Nelson processed!
    Record 561 for Boguchany processed!
    Record 562 for Sao Jose da Coroa Grande processed!
    Record 563 for Vardo processed!
    Record 564 for Pervomayskoye processed!
    Record 565 for Fernie processed!
    Record 566 for Bonthe processed!
    Record 567 for Victor Harbor processed!
    Record 568 for Kloulklubed processed!
    Record 569 for Bisert processed!
    Record 570 for Sept-Iles processed!
    Record 571 for Payo processed!
    Record 572 for Solwezi processed!
    Record 573 for Caramoran processed!
    Record 574 for Northam processed!
    Record 575 for Tadine processed!
    Record 576 for Armizonskoye processed!
    Record 577 for Auki processed!
    Record 578 for Rio Gallegos processed!
    Record 579 for Noumea processed!
    Record 580 for Dumai processed!
    Record 581 for Den Helder processed!
    Record 582 for Tarko-Sale processed!
    Record 583 for Otane processed!
    Record 584 for Irbit processed!
    Record 585 for Jining processed!
    Record 586 for Gizo processed!
    Record 587 for Kikwit processed!
    Record 588 for Mingshui processed!
    Record 589 for Coari processed!
    Record 590 for Tura processed!
    Record 591 for Weihai processed!
    Record 592 for Toora-Khem processed!
    Record 593 for Atasu processed!
    Record 594 for Florence processed!
    Record 595 for Dunedin processed!
    Record 596 for Jibert processed!
    Record 597 for Vanavara processed!
    Record 598 for Turayf processed!
    Record 599 for Ereymentau processed!
    Record 600 for North Auburn processed!
    Record 601 for Imbituba processed!
    Record 602 for Nikolayevsk-na-amure processed!
    Record 603 for North Bend processed!
    Record 604 for Lorengau processed!
    Record 605 for Kerema processed!
    Record 606 for Ipatovo processed!
    Record 607 for Trincomalee processed!
    Record 608 for Faya processed!
    Record 609 for Humenne processed!
    Record 610 for Mbini processed!
    Record 611 for Camara de Lobos processed!
    Record 612 for Saint-Joseph processed!
    Record 613 for Ribeira Grande processed!
    Record 614 for Bahia Honda processed!
    Record 615 for Valdivia processed!
    Record 616 for Alice Springs processed!
    Record 617 for Zhangye processed!
    Record 618 for Broken Hill processed!
    Record 619 for Hualmay processed!
    Record 620 for Gunnedah processed!
    Record 621 for Baker City processed!
    Record 622 for Jumla processed!
    Record 623 for Oranjemund processed!
    Record 624 for Koulamoutou processed!
    Record 625 for Lai processed!
    Record 626 for Jinxiang processed!
    Record 627 for San Angelo processed!
    Record 628 for Ondjiva processed!
    Record 629 for Berlevag processed!
    Record 630 for Remanso processed!
    Record 631 for Boda processed!
    Record 632 for Bainbridge processed!
    Record 633 for Bogorodskoye processed!
    Record 634 for Popondetta processed!
    Record 635 for Rurrenabaque processed!
    Record 636 for Dickinson processed!
    Record 637 for Gazli processed!
    Record 638 for Marystown processed!
    Record 639 for Morant Bay processed!
    Record 640 for Venado Tuerto processed!
    Record 641 for Kilimatinde processed!
    Record 642 for Sabang processed!
    Record 643 for Rosetta processed!
    Record 644 for Sur processed!
    Record 645 for Rypefjord processed!
    Record 646 for Sovetskaya processed!
    Record 647 for Aswan processed!
    Record 648 for Ingham processed!
    Record 649 for Toktogul processed!
    Record 650 for Craigieburn processed!
    Record 651 for Roald processed!
    Record 652 for Ahipara processed!
    Record 653 for Owando processed!
    Record 654 for Randazzo processed!
    Record 655 for Aldama processed!
    Record 656 for Kailua processed!
    Record 657 for Svetlogorsk processed!
    Record 658 for Massena processed!
    Record 659 for Hirara processed!
    Record 660 for Mogok processed!
    Record 661 for Taltal processed!
    Record 662 for Santo Antonio do Amparo processed!
    Record 663 for Puerto Colombia processed!
    Record 664 for Bluff processed!
    Record 665 for Matara processed!
    Record 666 for Dubna processed!
    Record 667 for Yar-Sale processed!
    Record 668 for Oum Hadjer processed!
    Record 669 for Aranda de Duero processed!
    Record 670 for Juneau processed!
    Record 671 for Kununurra processed!
    Record 672 for Arica processed!
    Record 673 for Pandan processed!
    Record 674 for Zhigansk processed!
    Record 675 for Humaita processed!
    Record 676 for Chiusi processed!
    Record 677 for Angol processed!
    Record 678 for Hibbing processed!
    Record 679 for Leshukonskoye processed!
    Record 680 for Biak processed!
    Record 681 for Dubbo processed!
    Record 682 for Axim processed!
    Record 683 for Chapais processed!
    Record 684 for San Policarpo processed!
    Record 685 for Andros Town processed!
    Record 686 for Ust-Kut processed!
    Record 687 for Hailar processed!
    Record 688 for El Dorado processed!
    Record 689 for Lerici processed!
    Record 690 for Hacienda Heights processed!
    Record 691 for Salisbury processed!
    Record 692 for Dwarka processed!
    Record 693 for Ojinaga processed!
    Record 694 for Southbridge processed!
    Record 695 for Saint Anthony processed!
    Record 696 for Kiunga processed!
    Record 697 for Betwagan processed!
    Record 698 for Methoni processed!
    Record 699 for Kwekwe processed!
    Record 700 for Nizhniy Bestyakh processed!
    Record 701 for Oskarshamn processed!
    Record 702 for Longhua processed!
    Record 703 for Kota processed!
    Record 704 for Blagoveshchenka processed!
    Record 705 for Deputatskiy processed!
    Record 706 for Ystad processed!
    Record 707 for Hikari processed!
    Record 708 for Sinaloa processed!
    Record 709 for Tessalit processed!
    Record 710 for Nouadhibou processed!
    Record 711 for Mildura processed!
    Record 712 for Brandon processed!
    Record 713 for Haverhill processed!
    Record 714 for Chitipa processed!
    Record 715 for Isla Mujeres processed!
    Record 716 for Ulaangom processed!
    Record 717 for Ust-Kuyga processed!
    Record 718 for Rocha processed!
    Record 719 for Parkes processed!
    Record 720 for Melito di Porto Salvo processed!
    Record 721 for Havre processed!
    Record 722 for Vila processed!
    Record 723 for Tabou processed!
    Record 724 for Scarborough processed!
    Record 725 for Arraias processed!
    Record 726 for Batsfjord processed!
    Record 727 for Harper processed!
    Record 728 for Mogocha processed!
    Record 729 for De Aar processed!
    Record 730 for Ivankiv processed!
    Record 731 for Montepuez processed!
    Record 732 for Nantucket processed!
    Record 733 for Sampit processed!
    Record 734 for Ponnampet processed!
    Record 735 for Darnah processed!
    Record 736 for Half Moon Bay processed!
    Record 737 for Santiago processed!
    Record 738 for Florida processed!
    Record 739 for Banepa processed!
    Record 740 for Sayville processed!
    Record 741 for Praia da Vitoria processed!
    Record 742 for Mogadishu processed!
    Record 743 for Kushiro processed!
    Record 744 for Richards Bay processed!
    Record 745 for Nardaran processed!
    Record 746 for Boali processed!
    Record 747 for Urdoma processed!
    Record 748 for Pontianak processed!
    Record 749 for Antofagasta processed!
    Record 750 for Mocuba processed!
    Record 751 for Harer processed!
    Record 752 for Moroto processed!
    Record 753 for Turgoyak processed!
    Record 754 for Mandurah processed!
    Record 755 for Meulaboh processed!
    Record 756 for Burns Lake processed!
    Record 757 for Jinka processed!
    Record 758 for Pinega processed!
    Record 759 for Aykhal processed!
    Record 760 for Moville processed!
    Record 761 for Severo-Yeniseyskiy processed!
    Record 762 for Laguna processed!
    Record 763 for Muzhi processed!
    Record 764 for Bay City processed!
    Record 765 for Jasper processed!
    Record 766 for Plouzane processed!
    Record 767 for Ichhawar processed!
    Record 768 for Goya processed!
    Record 769 for Coihueco processed!
    Record 770 for Le Pradet processed!
    Record 771 for Pelym processed!
    Record 772 for Syamzha processed!
    Record 773 for Strezhevoy processed!
    Record 774 for Timra processed!
    Record 775 for Sibu processed!
    Record 776 for Canton processed!
    Record 777 for Fairview processed!
    Record 778 for Lahij processed!
    Record 779 for Talcahuano processed!
    Record 780 for Finschhafen processed!
    Record 781 for Nioro processed!
    Record 782 for Batie processed!
    Record 783 for Linjiang processed!
    Record 784 for Salamiyah processed!
    Record 785 for Azare processed!
    Record 786 for Mokhsogollokh processed!
    Record 787 for Guangyuan processed!
    Record 788 for Kipushi processed!
    Record 789 for Sikasso processed!
    Record 790 for Gorno-Altaysk processed!
    Record 791 for Girona processed!
    Record 792 for Kencong processed!
    Record 793 for Tocopilla processed!
    Record 794 for Tanout processed!
    Record 795 for Hit processed!
    Record 796 for Dmytrivka processed!
    Record 797 for Ambunti processed!
    Record 798 for Igrim processed!
    Record 799 for Abu Samrah processed!
    Record 800 for Jiangyou processed!
    Record 801 for Voh processed!
    Record 802 for Suntar processed!
    Record 803 for High Level processed!
    Record 804 for Mingaora processed!
    Record 805 for Grand Gaube processed!
    Record 806 for Canico processed!
    Record 807 for Ahtopol processed!
    Record 808 for Sao Joao da Barra processed!
    Record 809 for Dzerzhinsk processed!
    Record 810 for Yanam processed!
    Record 811 for Pisco processed!
    Record 812 for Kedrovyy processed!
    Record 813 for Goias processed!
    Record 814 for San Pedro processed!
    Record 815 for Velyka Mykhaylivka processed!
    Record 816 for Alexandria processed!
    Record 817 for Tupancireta processed!
    Record 818 for Thinadhoo processed!
    Record 819 for Shelburne processed!
    Record 820 for Mayor Pablo Lagerenza processed!
    Record 821 for Urusha processed!
    Record 822 for Tadpatri processed!
    Record 823 for Tuscaloosa processed!
    Record 824 for Ibipeba processed!
    Record 825 for Novobirilyussy processed!
    Record 826 for Qena processed!
    Record 827 for Bud processed!
    Record 828 for Beringovskiy processed!
    Record 829 for Itacarambi processed!
    Record 830 for Bridlington processed!
    Record 831 for Omsukchan processed!
    Record 832 for Bambanglipuro processed!
    Record 833 for Payson processed!
    Record 834 for Beatrice processed!
    Record 835 for Skagen processed!
    Record 836 for Knysna processed!
    Record 837 for Murgab processed!
    Record 838 for Mafeteng processed!
    Record 839 for Lagos processed!
    Record 840 for Subtanjalla processed!
    Record 841 for Berdigestyakh processed!
    Record 842 for Bay Roberts processed!
    Record 843 for Whitehorse processed!
    Record 844 for Cuauhtemoc processed!
    Record 845 for Sault Sainte Marie processed!


### Create Dataframe and Count Rows


```python
# Create dictionary of lists

dict = {"City":name_list, "Latitude":latitude, "Temperature":temperature, "Humidity":humidity, "Cloudiness":cloudiness, "Wind Speed":wind_speed}

# Create dataframe from dictionary of lists

df = pd.DataFrame(dict)

# Arrange columns in dataframe

df = df[['City', 'Latitude', 'Temperature', 'Humidity', 'Cloudiness', 'Wind Speed']]

# Print non-null row count for columns in dataframe

print(df.count())

# Print dataframe to CSV

df.to_csv("World Cities Data")
```

    City           845
    Latitude       845
    Temperature    845
    Humidity       845
    Cloudiness     845
    Wind Speed     845
    dtype: int64


### What does my dataframe look like?


```python
# Print first 5 rows of dataframe

df.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Latitude</th>
      <th>Temperature</th>
      <th>Humidity</th>
      <th>Cloudiness</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Boden</td>
      <td>65.83</td>
      <td>17.60</td>
      <td>85</td>
      <td>88</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Naze</td>
      <td>5.43</td>
      <td>78.80</td>
      <td>88</td>
      <td>40</td>
      <td>6.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Maningrida</td>
      <td>-12.05</td>
      <td>77.75</td>
      <td>87</td>
      <td>8</td>
      <td>4.83</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Qaqortoq</td>
      <td>60.72</td>
      <td>21.20</td>
      <td>44</td>
      <td>40</td>
      <td>10.29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Srednekolymsk</td>
      <td>67.46</td>
      <td>-3.98</td>
      <td>65</td>
      <td>56</td>
      <td>5.35</td>
    </tr>
  </tbody>
</table>

### Latitude vs. Temperature Plot


```python
# Create plot of latitude vs. temperature

plt.scatter(df["Latitude"], df["Temperature"], marker="o")
plt.title("Temperature in World Cities")
plt.ylabel("Temperature (Fahrenheit)")
plt.xlabel("Latitude")
plt.grid(True)
plt.savefig("Temperature_In_World_Cities.png")
```


![png](output_12_0.png)


### Latitude vs. Humidity Plot


```python
# Create plot of latitude vs. humidity

plt.scatter(df["Latitude"], df["Humidity"], marker="o")
plt.title("Humidity in World Cities")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.savefig("Humidity_In_World_Cities.png")
```


![png](output_14_0.png)


### Latitude vs. Cloudiness Plot


```python
# Create plot of latitude vs. cloudiness

plt.scatter(df["Latitude"], df["Cloudiness"], marker="o")
plt.title("Cloudiness in World Cities")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.savefig("Cloudiness_In_World_Cities.png")
```


![png](output_16_0.png)


### Wind Speed in World Cities


```python
# Create plot of latitude vs. wind speed

plt.scatter(df["Latitude"], df["Wind Speed"], marker="o")
plt.title("Wind Speed in World Cities")
plt.ylabel("Wind Speed (MPH)")
plt.xlabel("Latitude")
plt.grid(True)
plt.savefig("Wind_Speed_In_World_Cities.png")
```


![png](output_18_0.png)

