```
https://www.cloudskillsboost.google/focuses/1846?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15211841
```



```
&cloudshell=true
```

```bash
gcloud compute instances create instance-1 --project=$DEVSHELL_PROJECT_ID --zone=us-central1-a --machine-type=e2-medium --network-interface=network-tier=PREMIUM,subnet=default --metadata=enable-oslogin=true --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/cloud-platform --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/debian-cloud/global/images/debian-10-buster-v20220118,mode=rw,size=10,type=projects/$DEVSHELL_PROJECT_ID/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

```


```bash
gcloud beta compute ssh --zone "us-central1-a" "instance-1" --project $DEVSHELL_PROJECT_ID
```

<!-- ```bash
git clone https://github.com/GoogleCloudPlatform/training-data-analyst

```

```bash
yes 'Y' | sudo apt-get update
yes 'Y' | sudo apt-get -y -qq install git
yes 'Y' | sudo apt-get install python-mpltoolkits.basemap
cd training-data-analyst/CPB100/lab2b
yes 'Y' | bash ingest.sh
yes 'Y' | bash install_missing.sh
python3 transform.py
export BUCK=$(cat /dev/urandom | tr -dc 'a-z0-9' | fold -w 63 | head -n 1)
gsutil mb gs://$BUCK
gsutil cp earthquakes.* gs://$BUCK/earthquakes/


``` -->


```
mkdir training-data-analyst
cd training-data-analyst
mkdir CPB100
cd CPB100
mkdir lab2b
cd lab2b

echo 'time,latitude,longitude,depth,mag,magType,nst,gap,dmin,rms,net,id,updated,place,type,horizontalError,depthError,magError,magNst,status,locationSource,magSource
2022-01-23T05:57:45.943Z,38.2499,-118.3542,1.5,0.3,ml,8,162.12,0.118,0.2633,nn,nn00832260,2022-01-23T06:01:45.614Z,"26 km SW of Mina, Nevada",earthquake,,4.7,0.18,3,automatic,nn,nn
2022-01-23T05:31:50.426Z,38.2614,-118.3549,10.4,1.7,ml,20,85.24,0.118,0.2093,nn,nn00832257,2022-01-23T05:35:28.601Z,"California-Nevada border region",earthquake,,0.5,0.2,11,automatic,nn,nn
2022-01-23T05:21:24.100Z,34.1711667,-117.5905,8.1,1.18,ml,26,87,0.06396,0.19,ci,ci39920895,2022-01-23T05:24:57.001Z,"5km N of Rancho Cucamonga, CA",earthquake,0.43,0.85,0.368,34,automatic,ci,ci
2022-01-23T05:14:49.850Z,35.0591667,-119.1848333,10,1.87,ml,27,78,0.211,0.26,ci,ci39920887,2022-01-23T05:18:40.969Z,"20km E of Maricopa, CA",earthquake,0.43,1.37,0.196,28,automatic,ci,ci
2022-01-23T05:09:25.573Z,38.2505,-118.3504,0.1,0.7,ml,8,161.63,0.121,0.2225,nn,nn00832256,2022-01-23T05:15:35.487Z,"26 km SW of Mina, Nevada",earthquake,,9.8,0.17,4,automatic,nn,nn
2022-01-23T04:49:40.000Z,35.0603333,-119.193,10.95,2.02,ml,33,70,0.2044,0.28,ci,ci39920871,2022-01-23T05:00:17.920Z,"19km E of Maricopa, CA",earthquake,0.41,1.12,0.115,27,automatic,ci,ci
2022-01-23T04:47:29.710Z,19.2211666107178,-155.38916015625,31.3600006103516,1.83000004,md,32,159,,0.119999997,hv,hv72886792,2022-01-23T04:50:41.800Z,"9 km ENE of Pāhala, Hawaii",earthquake,0.71,1.05999994,0.910000026,3,automatic,hv,hv
2022-01-23T04:30:52.387Z,38.1478,46.2103,10,4.1,mb,,89,2.58,0.87,us,us7000geby,2022-01-23T05:48:26.836Z,"10 km NW of Tabriz, Iran",earthquake,8.6,2,0.145,13,reviewed,us,us
2022-01-23T04:15:58.400Z,38.7989998,-122.7788315,0.59,2.34,md,28,56,0.01568,0.23,nc,nc73682161,2022-01-23T04:52:11.244Z,"3km NW of The Geysers, CA",earthquake,0.42,0.66,0.14,28,automatic,nc,nc
2022-01-23T04:12:32.066Z,-13.9895,-70.55,10,4.3,mb,,146,3.267,0.88,us,us7000gebs,2022-01-23T04:40:47.040Z,"14 km SSE of Corani, Peru",earthquake,11.2,2,0.142,14,reviewed,us,us
2022-01-23T03:58:52.297Z,38.5353,97.3907,10,4.2,mb,,77,11.376,0.85,us,us7000gebn,2022-01-23T04:14:13.040Z,"147 km SSW of Laojunmiao, China",earthquake,10.6,2,0.107,24,reviewed,us,us
2022-01-23T03:35:37.440Z,19.1681671142578,-155.48649597168,35.2200012207031,2.6099999,md,44,98,,0.109999999,hv,hv72886727,2022-01-23T03:38:57.620Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.56,1,0.689999998,24,automatic,hv,hv
2022-01-23T03:07:36.404Z,38.152,-118.0308,1.4,0.8,ml,9,144.43,0.058,0.0783,nn,nn00832253,2022-01-23T03:11:15.161Z,"27 km SSE of Mina, Nevada",earthquake,,0.8,0.33,5,automatic,nn,nn
2022-01-23T03:00:12.855Z,61.7139,-150.4908,61.6,1.8,ml,,,,0.65,ak,ak0221235b5x,2022-01-23T03:03:01.280Z,"19 km N of Susitna, Alaska",earthquake,,1.2,,,automatic,ak,ak
2022-01-23T02:48:57.140Z,19.1630001068115,-155.493667602539,34.8699989318848,2.06999993,md,36,112,,0.109999999,hv,hv72886672,2022-01-23T02:52:12.970Z,"4 km SSW of Pāhala, Hawaii",earthquake,0.45,0.769999981,1.77999997,14,automatic,hv,hv
2022-01-23T02:38:52.590Z,19.1636657714844,-155.490173339844,34.7299995422363,2.57,ml,47,147,,0.109999999,hv,hv72886657,2022-01-23T02:48:42.040Z,"4 km SSW of Pāhala, Hawaii",earthquake,0.6,0.920000017,3.8,18,automatic,hv,hv
2022-01-23T02:31:49.260Z,37.4501667,-118.8128333,3.81,1.29,md,22,78,0.1284,0.04,nc,nc73682151,2022-01-23T04:37:11.153Z,"17km SW of Toms Place, CA",earthquake,0.25,1.74,0.116,15,reviewed,nc,nc
2022-01-23T02:31:26.494Z,63.4775,-148.8374,1.6,1.9,ml,,,,0.5,ak,ak022122qjss,2022-01-23T02:41:18.855Z,"11 km NNE of Cantwell, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-23T02:21:19.787Z,38.4843,97.3967,10,5.6,mww,,32,11.416,0.93,us,us7000gebb,2022-01-23T04:24:55.590Z,"152 km S of Laojunmiao, China",earthquake,7.9,1.8,0.059,28,reviewed,us,us
2022-01-23T02:19:06.971Z,38.2527,-118.3459,0,0.8,ml,8,160.23,0.125,0.1968,nn,nn00832252,2022-01-23T02:37:44.070Z,"25 km SW of Mina, Nevada",earthquake,,9.9,0.22,4,automatic,nn,nn
2022-01-23T02:17:45.030Z,19.1720008850098,-155.487503051758,34.310001373291,2.13000011,md,28,145,,0.109999999,hv,hv72886632,2022-01-23T02:20:59.600Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.67,1.00999999,1.21000004,7,automatic,hv,hv
2022-01-23T02:16:15.167Z,38.2667,-118.3626,9.7,1.4,ml,14,138.04,0.113,0.0824,nn,nn00832250,2022-01-23T02:37:20.143Z,"26 km WSW of Mina, Nevada",earthquake,,0.7,0.11,8,automatic,nn,nn
2022-01-23T02:15:11.902Z,63.1276,-151.3681,0,1.7,ml,,,,0.65,ak,ak022122n39j,2022-01-23T02:28:36.896Z,"Central Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-23T02:10:24.100Z,63.3131,-145.0044,7.6,1.3,ml,,,,0.65,ak,ak022122m1l5,2022-01-23T02:19:05.117Z,"39 km NE of Paxson, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-23T02:07:21.694Z,38.2507,-118.3625,4.1,1.1,ml,12,147.92,0.112,0.0997,nn,nn00832248,2022-01-23T02:37:05.138Z,"27 km SW of Mina, Nevada",earthquake,,2.5,0.34,5,automatic,nn,nn
2022-01-23T02:01:18.451Z,38.0544,-118.6109,0,1.4,ml,11,210.66,0.214,0.1519,nn,nn00832247,2022-01-23T03:42:11.859Z,"28 km NNW of Benton, California",earthquake,,11.4,0.19,8,automatic,nn,nn
2022-01-23T02:00:06.906Z,38.5496,-119.4946,8.1,1.5,ml,10,163.49,0.041,0.4987,nn,nn00832246,2022-01-23T02:36:56.907Z,"2 km SSE of Coleville, California",earthquake,,0.7,0.42,5,automatic,nn,nn
2022-01-23T01:39:23.534Z,38.2532,-118.3643,1.2,0.8,ml,8,160.37,0.11,0.1043,nn,nn00832245,2022-01-23T01:43:34.094Z,"27 km SW of Mina, Nevada",earthquake,,4.7,0.22,3,automatic,nn,nn
2022-01-23T01:34:36.460Z,38.7714996,-122.7249985,-0.73,1.94,md,10,125,0.05408,0.09,nc,nc73682136,2022-01-23T02:46:10.631Z,"3km ESE of The Geysers, CA",earthquake,0.46,1.21,0.08,9,automatic,nc,nc
2022-01-23T01:28:05.650Z,19.1708335876465,-155.494659423828,34.9900016784668,2.1500001,md,33,97,,0.119999997,hv,hv72886582,2022-01-23T01:31:32.120Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.59,0.689999998,1.39999998,10,automatic,hv,hv
2022-01-23T01:20:27.640Z,38.8230019,-122.8115005,3.14,2.52,md,23,65,0.01963,0.13,nc,nc73682126,2022-01-23T02:21:11.505Z,"7km NW of The Geysers, CA",earthquake,0.33,0.56,0.09,25,automatic,nc,nc
2022-01-23T01:20:10.260Z,38.5410004,-119.5333328,5.43,2.63,md,11,89,0.04609,0.08,nc,nc73682121,2022-01-23T02:06:11.429Z,"6km WNW of Walker, CA",earthquake,0.49,1.42,0.26,19,automatic,nc,nc
2022-01-23T01:20:08.745Z,38.5399,-119.5347,0,2.4,ml,14,145.51,0.205,0.3192,nn,nn00832240,2022-01-23T01:23:54.838Z,"3 km SW of Coleville, California",earthquake,,18.7,0.26,11,automatic,nn,nn
2022-01-23T01:18:09.850Z,19.1596660614014,-155.487167358398,33.3899993896484,2.00999999,md,35,120,,0.140000001,hv,hv72886567,2022-01-23T01:21:18.080Z,"4 km S of Pāhala, Hawaii",earthquake,0.68,1.14999998,1.82000005,10,automatic,hv,hv
2022-01-23T01:12:36.631Z,3.5827,126.7536,50.1,4.7,mb,,98,2.858,0.92,us,us7000geaz,2022-01-23T02:42:08.040Z,"247 km SE of Sarangani, Philippines",earthquake,7.3,7.3,0.06,85,reviewed,us,us
2022-01-23T01:06:45.309Z,61.513,-149.9429,32.3,1.5,ml,,,,0.45,ak,ak022121zsr7,2022-01-23T01:16:58.233Z,"1 km SSE of Big Lake, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-23T00:58:49.733Z,36.8212,-115.883,4.9,1.2,ml,14,134.24,0.124,0.2689,nn,nn00832238,2022-01-23T01:01:54.451Z,"33 km NW of Indian Springs, Nevada",earthquake,,1.8,0.2,10,automatic,nn,nn
2022-01-23T00:57:23.107Z,38.4196,138.3185,18.41,4.3,mb,,137,1.872,0.42,us,us7000geay,2022-01-23T01:31:52.040Z,"39 km NNW of Ryōtsu-minato, Japan",earthquake,7.5,5.3,0.137,15,reviewed,us,us
2022-01-23T00:51:50.810Z,38.2507,-118.3523,0.8,1,ml,8,161.54,0.12,0.21,nn,nn00832237,2022-01-23T00:56:03.687Z,"26 km SW of Mina, Nevada",earthquake,,9.8,0.15,4,automatic,nn,nn
2022-01-23T00:45:20.408Z,34.5616,26.33,36.45,4.7,mb,,45,1.387,0.88,us,us7000geaw,2022-01-23T03:34:42.005Z,"70 km S of Palekastro, Greece",earthquake,5.9,7.1,0.052,113,reviewed,us,us
2022-01-23T00:42:46.300Z,38.2497,-118.3613,0,1.3,ml,12,148.47,0.113,0.2282,nn,nn00832235,2022-01-23T00:46:14.040Z,"27 km SW of Mina, Nevada",earthquake,,6.2,0.17,7,automatic,nn,nn
2022-01-23T00:37:38.989Z,38.2134,-118.3535,11.4,1.4,ml,10,161.17,0.125,0.4443,nn,nn00832234,2022-01-23T00:41:33.801Z,"29 km SW of Mina, Nevada",earthquake,,0.5,0.58,6,automatic,nn,nn
2022-01-23T00:20:02.080Z,38.2496,-118.3619,9.3,1.4,ml,12,148.52,0.112,0.3199,nn,nn00832232,2022-01-23T00:23:23.817Z,"27 km SW of Mina, Nevada",earthquake,,0.8,0.25,8,automatic,nn,nn
2022-01-23T00:14:14.121Z,38.2546,-118.3658,6.9,2.1,ml,22,67.06,0.109,0.243,nn,nn00832229,2022-01-23T00:18:04.903Z,"27 km SW of Mina, Nevada",earthquake,,0.5,0.29,12,automatic,nn,nn
2022-01-23T00:01:43.182Z,38.2188,-118.363,9.6,1.1,ml,10,181.08,0.116,0.3612,nn,nn00832228,2022-01-23T00:05:33.418Z,"29 km SW of Mina, Nevada",earthquake,,1,0.25,6,automatic,nn,nn
2022-01-22T23:53:55.999Z,60.3369,-147.7607,18.1,2.3,ml,,,,0.89,ak,ak02210ru308,2022-01-23T00:08:00.608Z,"33 km NNE of Chenega, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-22T23:51:16.834Z,38.2505,-118.3583,10.4,2.9,ml,25,63.79,0.115,0.1414,nn,nn00832225,2022-01-23T02:37:51.303Z,"26 km SW of Mina, Nevada",earthquake,,1.4,0.31,8,reviewed,nn,nn
2022-01-22T23:46:49.192Z,61.5445,-146.7612,0,1.7,ml,,,,1.4,ak,ak02210rskif,2022-01-22T23:52:38.738Z,"48 km SSE of Eureka Roadhouse, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-22T23:44:21.000Z,19.2553329467773,-155.435836791992,31.4300003051758,1.97,ml,40,112,,0.150000006,hv,hv72886497,2022-01-22T23:49:52.640Z,"7 km NE of Pāhala, Hawaii",earthquake,0.53,0.889999986,2.81,6,automatic,hv,hv
2022-01-22T23:43:05.270Z,34.9466667,-118.5371667,2.08,2.21,ml,34,47,0.1665,0.23,ci,ci39920807,2022-01-22T23:54:16.010Z,"20km NNE of Neenach, CA",earthquake,0.29,1.4,0.212,27,automatic,ci,ci
2022-01-22T23:41:18.260Z,47.773,-120.793833333333,1.77,1.34,ml,18,59,0.103,0.26,uw,uw61812321,2022-01-23T05:23:56.900Z,"22 km NNW of Leavenworth, Washington",earthquake,0.47,1.67,0.131971541135902,8,reviewed,uw,uw
2022-01-22T23:37:07.566Z,38.1385,-118.2834,1.1,1.5,ml,8,205.41,0.207,0.3445,nn,nn00832224,2022-01-22T23:41:35.074Z,"31 km SSW of Mina, Nevada",earthquake,,20.1,0.09,3,automatic,nn,nn
2022-01-22T23:32:41.642Z,38.2788,-118.3287,16,1.6,ml,12,142.62,0.126,0.1494,nn,nn00832223,2022-01-22T23:36:58.548Z,"22 km WSW of Mina, Nevada",earthquake,,0.7,0.37,8,automatic,nn,nn
2022-01-22T23:31:07.314Z,63.2405,-150.7128,4.8,1.7,ml,,,,0.49,ak,ak02210rp9j4,2022-01-22T23:43:17.379Z,"60 km SE of Denali National Park, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-22T23:21:59.378Z,38.2418,-118.3482,0,1.2,ml,8,166.5,0.123,0.2237,nn,nn00832222,2022-01-22T23:26:14.953Z,"Nevada",earthquake,,9.8,0.11,4,automatic,nn,nn
2022-01-22T23:20:14.314Z,38.2532,-118.3592,10.6,2.1,ml,22,121.46,0.114,0.2233,nn,nn00832218,2022-01-22T23:23:40.819Z,"26 km SW of Mina, Nevada",earthquake,,0.4,0.28,12,automatic,nn,nn
2022-01-22T23:17:32.420Z,35.629,-117.418,8.49,1.1,ml,7,174,0.05564,0.08,ci,ci39920783,2022-01-22T23:20:59.609Z,"15km SSW of Trona, CA",earthquake,0.58,0.5,0.131,8,automatic,ci,ci
2022-01-22T23:17:16.252Z,38.2595,-118.3512,12.8,2.3,ml,22,79.83,0.121,0.2546,nn,nn00832215,2022-01-22T23:20:58.574Z,"25 km SW of Mina, Nevada",earthquake,,0.5,0.38,12,automatic,nn,nn
2022-01-22T23:14:36.682Z,62.8885,-150.3107,11.1,1.8,ml,,,,0.74,ak,ak02210rlomu,2022-01-22T23:26:25.402Z,"49 km NNE of Petersville, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-22T23:10:36.820Z,36.3116684,-120.8458328,13.73,1.19,md,4,176,0.1797,0,nc,nc73682086,2022-01-22T23:27:13.377Z,"19km SW of New Idria, CA",earthquake,0.82,2.66,0.32,2,automatic,nc,nc
2022-01-22T23:09:04.142Z,38.2587,-118.3585,7.7,1.3,ml,12,142.85,0.115,0.0628,nn,nn00832214,2022-01-22T23:12:48.735Z,"26 km SW of Mina, Nevada",earthquake,,1.4,0.14,7,automatic,nn,nn
2022-01-22T23:08:44.030Z,19.2018337249756,-155.426330566406,33.2700004577637,2.33,ml,37,144,,0.239999995,hv,hv72886462,2022-01-22T23:14:14.730Z,"5 km E of Pāhala, Hawaii",earthquake,0.67,1.04999995,3.7,4,automatic,hv,hv
2022-01-22T23:07:30.250Z,35.8075,-118.5056667,8.06,1.35,ml,16,80,0.08138,0.15,ci,ci39920775,2022-01-22T23:11:09.029Z,"9km NW of Kernville, CA",earthquake,0.37,1.04,0.132,16,automatic,ci,ci
2022-01-22T23:03:57.099Z,38.2709,-118.3443,12.2,1.9,ml,17,84.21,0.135,0.1082,nn,nn00832212,2022-01-22T23:07:42.686Z,"California-Nevada border region",earthquake,,0.6,0.22,8,automatic,nn,nn
2022-01-22T23:03:12.020Z,32.9683333,-115.5571667,4.69,1.53,ml,15,96,0.06675,0.2,ci,ci39920767,2022-01-22T23:06:51.848Z,"3km WSW of Brawley, CA",earthquake,0.45,1.03,0.213,20,automatic,ci,ci
2022-01-22T23:02:29.871Z,38.2375,-118.3651,7.3,1,ml,8,170.09,0.111,0.292,nn,nn00832211,2022-01-22T23:06:35.713Z,"28 km SW of Mina, Nevada",earthquake,,2.1,0.12,5,automatic,nn,nn
2022-01-22T22:58:38.068Z,38.2652,-118.3472,10,1.8,ml,16,125.64,0.125,0.2055,nn,nn00832207,2022-01-22T23:02:22.714Z,"25 km SW of Mina, Nevada",earthquake,,0.5,0.21,8,automatic,nn,nn
2022-01-22T22:57:21.443Z,38.2395,-118.3639,9.8,2.1,ml,18,139.35,0.111,0.2763,nn,nn00832204,2022-01-22T23:01:16.635Z,"27 km SW of Mina, Nevada",earthquake,,0.6,0.32,11,automatic,nn,nn
2022-01-22T22:55:47.222Z,38.2593,-118.3552,11.1,2.5,ml,24,73.62,0.118,0.1854,nn,nn00832201,2022-01-22T22:59:41.897Z,"26 km SW of Mina, Nevada",earthquake,,0.4,0.29,13,automatic,nn,nn
2022-01-22T22:50:58.213Z,38.2628,-118.3494,10.3,1.9,ml,16,126.79,0.123,0.2145,nn,nn00832197,2022-01-22T22:54:28.359Z,"California-Nevada border region",earthquake,,0.6,0.21,9,automatic,nn,nn
2022-01-22T22:49:10.024Z,38.252,-118.3508,0.9,0.8,ml,8,160.76,0.121,0.1479,nn,nn00832196,2022-01-22T22:53:14.766Z,"26 km SW of Mina, Nevada",earthquake,,9.8,0.29,4,automatic,nn,nn
2022-01-22T22:46:43.149Z,38.2618,-118.3527,8.1,1.8,ml,17,127.28,0.12,0.1669,nn,nn00832193,2022-01-22T22:50:22.152Z,"25 km SW of Mina, Nevada",earthquake,,1,0.2,6,automatic,nn,nn
2022-01-22T22:45:42.546Z,38.262,-118.3489,10.3,2.1,ml,19,84.82,0.123,0.1931,nn,nn00832190,2022-01-22T22:49:36.326Z,"25 km SW of Mina, Nevada",earthquake,,0.5,0.18,8,automatic,nn,nn
2022-01-22T22:42:49.070Z,38.2692,-118.3396,9.1,1.9,ml,8,136.48,0.131,0.0372,nn,nn00832189,2022-01-22T22:48:38.371Z,"24 km SW of Mina, Nevada",earthquake,,6.1,0,2,automatic,nn,nn
2022-01-22T22:40:11.845Z,38.2571,-118.3528,11.7,4.3,mw,28,51.61,0.12,0.1561,nn,nn00832186,2022-01-23T03:02:46.140Z,"25 km SW of Mina, Nevada",earthquake,,1,,,reviewed,nn,nn
2022-01-22T22:18:27.220Z,38.7770004,-122.7348328,-0.75,1.61,md,9,98,0.05524,0.37,nc,nc73682041,2022-01-22T23:34:11.108Z,"2km E of The Geysers, CA",earthquake,2.28,5.8,0.08,8,automatic,nc,nc
2022-01-22T22:07:17.686Z,13.7376,120.8292,133.87,4.9,mb,,111,9.513,0.85,us,us7000gea5,2022-01-22T22:25:04.040Z,"6 km WNW of Bagalangit, Philippines",earthquake,7.9,6.1,0.05,124,reviewed,us,us
2022-01-22T22:02:49.490Z,37.5265,-118.4698333,7.96,1.43,md,17,57,0.0301,0.04,nc,nc73682031,2022-01-23T00:29:12.763Z,"16km NNW of Dixon Lane-Meadow Creek, CA",earthquake,0.43,0.89,0.073,12,reviewed,nc,nc
2022-01-22T21:48:27.199Z,-18.9534,169.3694,237.35,5.1,mb,,80,4.055,0.66,us,us7000ge9z,2022-01-22T22:01:12.040Z,"65 km N of Isangel, Vanuatu",earthquake,8.1,4,0.084,48,reviewed,us,us
2022-01-22T21:41:27.290Z,19.2078342437744,-155.391830444336,31.3099994659424,1.82000005,md,35,160,,0.119999997,hv,hv72886337,2022-01-22T21:44:40.950Z,"9 km E of Pāhala, Hawaii",earthquake,0.69,0.910000026,0.419999987,11,automatic,hv,hv
2022-01-22T21:36:54.104Z,32.5314,35.5634,10,4.1,mb,,251,2.006,0.94,us,us7000geaf,2022-01-23T06:23:04.129Z,"4 km WSW of Waqqāş, Jordan",earthquake,10.7,2,0.165,10,reviewed,us,us
2022-01-22T21:33:30.923Z,63.1106,-144.2624,1.5,2.3,ml,,,,0.68,ak,ak02210qivl7,2022-01-22T21:39:43.874Z,"32 km NW of Mentasta Lake, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-22T21:31:12.047Z,64.0482,-148.444,13.8,1.3,ml,,,,0.49,ak,ak02210qiep2,2022-01-22T21:35:52.962Z,"33 km E of Ferry, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-22T21:21:26.954Z,-20.4982,-175.3714,10,4.8,mb,,107,6.792,0.45,us,us7000gea6,2022-01-23T05:37:05.040Z,"73 km NNW of Nuku‘alofa, Tonga",earthquake,14.6,1.9,0.143,15,reviewed,us,us
2022-01-22T21:17:49.954Z,62.0883,-151.1706,66.3,1.5,ml,,,,0.99,ak,ak02210qfhkw,2022-01-22T21:21:31.155Z,"16 km NE of Skwentna, Alaska",earthquake,,1.3,,,automatic,ak,ak
2022-01-22T21:00:15.669Z,61.5903,-148.089,17.4,1.5,ml,,,,0.34,ak,ak02210qbrrt,2022-01-22T21:07:49.551Z,"30 km SE of Chickaloon, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-22T20:57:15.810Z,40.536499,-123.9926682,20.28,2.28,md,15,97,0.1541,0.09,nc,nc73682016,2022-01-22T21:19:11.178Z,"9km E of Hydesville, CA",earthquake,0.55,0.98,0.19,10,automatic,nc,nc
2022-01-22T20:45:32.740Z,19.1578330993652,-155.487167358398,33.25,2.06999993,md,35,126,,0.119999997,hv,hv72886262,2022-01-22T20:48:56.140Z,"5 km S of Pāhala, Hawaii",earthquake,0.61,1.00999999,0.970000029,11,automatic,hv,hv
2022-01-22T20:34:38.510Z,17.9911,-66.9638,9,2.94,md,22,154,0.0833,0.24,pr,pr2022022007,2022-01-22T21:31:38.185Z,"5 km W of Fuig, Puerto Rico",earthquake,0.4,0.62,0.33,17,reviewed,pr,pr
2022-01-22T20:08:59.478Z,58.1176,-155.8127,28.4,2.8,ml,,,,0.47,ak,ak02210ps8mk,2022-01-22T20:19:03.814Z,"80 km SE of King Salmon, Alaska",earthquake,,4.1,,,automatic,ak,ak
2022-01-22T20:08:47.246Z,57.1413,-155.486,35,2.8,ml,,173,0.704,0.47,us,us7000ge99,2022-01-23T00:36:34.040Z,"78 km SW of Karluk, Alaska",earthquake,5.9,2,0.053,46,reviewed,us,us
2022-01-22T20:03:45.911Z,-22.7477,-68.481,14.84,4.5,mb,,66,0.345,0.62,us,us7000ge96,2022-01-23T00:31:38.040Z,"33 km WNW of San Pedro de Atacama, Chile",earthquake,3.7,5,0.118,21,reviewed,us,us
2022-01-22T20:00:13.860Z,-22.8174,-68.4723,18.68,4.6,mwr,,37,0.302,1,us,us7000ge95,2022-01-22T20:36:25.040Z,"29 km WNW of San Pedro de Atacama, Chile",earthquake,4.8,4.6,,,reviewed,us,guc
2022-01-22T19:53:04.910Z,36.8440018,-121.5699997,4.47,1.26,md,9,192,0.04405,0.09,nc,nc73681996,2022-01-22T20:24:10.447Z,"3km W of San Juan Bautista, CA",earthquake,0.65,1.19,0.24,9,automatic,nc,nc
2022-01-22T19:45:57.000Z,17.983,-66.9685,9,2.42,md,12,165,0.0769,0.1,pr,pr2022022006,2022-01-22T20:17:01.926Z,"5 km W of Fuig, Puerto Rico",earthquake,0.37,0.7,0.21,8,reviewed,pr,pr
2022-01-22T19:31:43.008Z,39.5667,28.8303,3.01,4.7,mb,,26,0.751,0.87,us,us7000ge92,2022-01-23T00:13:29.323Z,"17 km E of Dursunbey, Turkey",earthquake,2.7,4.4,0.062,79,reviewed,us,us
2022-01-22T19:08:59.449Z,60.2101,-153.0844,122.2,0.8,ml,,,,0.26,ak,ak02210p6po8,2022-01-22T19:11:45.026Z,"68 km E of Port Alsworth, Alaska",earthquake,,1.9,,,automatic,ak,ak
2022-01-22T19:05:17.471Z,59.5395,-152.877,103.3,2.5,ml,,,,0.41,ak,ak02210p5z9u,2022-01-22T23:32:14.040Z,"57 km WNW of Nanwalek, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-22T18:59:54.930Z,34.036,-117.0443333,16.29,1.61,ml,45,65,0.05654,0.21,ci,ci39920623,2022-01-22T19:14:48.072Z,"0km NNW of Yucaipa, CA",earthquake,0.25,0.67,0.209,28,automatic,ci,ci
2022-01-22T18:48:08.090Z,36.3381667,-89.418,4.03,2.38,md,43,58,0.03595,0.23,nm,nm60380066,2022-01-22T20:23:14.869Z,"6 km SE of Tiptonville, Tennessee",earthquake,0.32,0.37,0.096,33,reviewed,nm,nm
2022-01-22T18:44:42.150Z,19.174165725708,-155.496002197266,33.8199996948242,2.38000011,md,41,139,,0.150000006,hv,hv72886147,2022-01-22T18:48:01.610Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.48,0.720000029,1.73000002,20,automatic,hv,hv
2022-01-22T18:28:35.270Z,36.5721664,-121.1151657,9.59,1.64,md,13,123,0.05654,0.11,nc,nc73681986,2022-01-22T19:02:11.049Z,"5km NNE of Pinnacles, CA",earthquake,0.46,1.1,0.21,14,automatic,nc,nc
2022-01-22T18:11:43.260Z,19.4909992218018,-155.274993896484,30.7999992370605,1.99000001,md,42,56,,0.109999999,hv,hv72886122,2022-01-22T18:17:13.920Z,"6 km NW of Volcano, Hawaii",earthquake,0.46,0.560000002,0.519999981,21,automatic,hv,hv
2022-01-22T18:04:26.500Z,55.5089,-155.707,48.2,3.7,ml,,,,0.73,ak,ak02210okdap,2022-01-22T19:22:50.337Z,"186 km SSW of Akhiok, Alaska",earthquake,,4.4,,,reviewed,ak,ak
2022-01-22T17:19:30.100Z,19.1893329620361,-155.508163452148,35.2400016784668,2.48,ml,48,75,,0.119999997,hv,hv72886087,2022-01-23T01:48:44.121Z,"3 km WSW of Pāhala, Hawaii",earthquake,0.54,0.74000001,4.1,19,automatic,hv,hv
2022-01-22T16:42:30.250Z,19.1668338775635,-155.482330322266,33.939998626709,1.84000003,md,30,104,,0.180000007,hv,hv72886052,2022-01-22T16:45:55.980Z,"4 km S of Pāhala, Hawaii",earthquake,0.76,1.20000005,0.920000017,3,automatic,hv,hv
2022-01-22T16:33:39.730Z,19.1634998321533,-155.472671508789,31.4699993133545,1.90999997,md,33,161,,0.140000001,hv,hv72886047,2022-01-22T16:36:54.930Z,"4 km S of Pāhala, Hawaii",earthquake,0.49,0.829999983,0.949999988,3,automatic,hv,hv
2022-01-22T16:24:13.820Z,63.4886,-148.4126,7.6,1.6,ml,,,,0.53,ak,ak02210nhqsm,2022-01-22T16:30:06.861Z,"28 km ENE of Cantwell, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-22T16:23:22.970Z,19.1979999542236,-155.476837158203,35.4300003051758,2.61,ml,45,86,,0.100000001,hv,hv72886042,2022-01-22T17:46:26.040Z,"0 km SSE of Pāhala, Hawaii",earthquake,0.47,0.680000007,4.09,23,automatic,hv,hv
2022-01-22T16:12:59.300Z,38.8203316,-122.8133316,1.33,1.3,md,8,83,0.003979,0.03,nc,nc73681981,2022-01-22T16:46:11.004Z,"7km NW of The Geysers, CA",earthquake,0.39,0.81,,1,automatic,nc,nc
2022-01-22T16:04:23.597Z,61.0479,-146.3343,10.7,2.4,ml,,,,1.04,ak,ak02210ndh63,2022-01-22T16:10:14.491Z,"9 km S of Valdez, Alaska",earthquake,,0.1,,,automatic,ak,ak
2022-01-22T15:33:45.292Z,63.3627,-151.1128,13.9,1.7,ml,,,,0.65,ak,ak02210myah5,2022-01-22T15:40:41.003Z,"36 km ESE of Denali National Park, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-22T15:23:26.105Z,61.5976,-149.817,47.7,1.9,ml,,,,0.24,ak,ak02210mw4f6,2022-01-22T15:26:19.285Z,"3 km S of Houston, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-22T15:22:06.911Z,38.1481,-117.9967,11.1,0.7,ml,9,152.53,0.031,0.1116,nn,nn00832185,2022-01-22T15:25:56.597Z,"28 km SSE of Mina, Nevada",earthquake,,0.6,0.27,4,automatic,nn,nn
2022-01-22T15:18:06.152Z,-5.9458,-12.4727,10,5.1,mb,,60,2.721,0.69,us,us7000ge87,2022-01-22T15:37:16.040Z,"Ascension Island region",earthquake,12,1.9,0.067,73,reviewed,us,us
2022-01-22T15:09:40.335Z,62.961,-150.3342,93.2,1.5,ml,,,,0.21,ak,ak02210mt5ht,2022-01-22T15:12:27.403Z,"56 km NNE of Petersville, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-22T15:06:28.409Z,60.8989,-148.6145,7.2,2.1,ml,,,,0.5,ak,ak02210mshi8,2022-01-22T15:26:19.140Z,"14 km NNE of Whittier, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-22T15:02:05.258Z,-23.8622,-67.0322,246.87,4.4,mb,,88,1.389,0.74,us,us7000ge7z,2022-01-22T16:44:42.040Z,"82 km WNW of San Antonio de los Cobres, Argentina",earthquake,9.3,9.3,0.156,13,reviewed,us,us
2022-01-22T14:48:17.316Z,-44.1132,-82.083,10,5.3,mww,,85,7.258,1.05,us,us7000ge7w,2022-01-22T17:54:12.040Z,"West Chile Rise",earthquake,9.9,1.8,0.053,34,reviewed,us,us
2022-01-22T14:38:19.470Z,46.1006666666667,-122.408666666667,16.67,0.53,ml,12,110,0.08597,0.24,uw,uw61812241,2022-01-23T05:53:04.480Z,"21 km N of Amboy, Washington",earthquake,1.26,1.56,0.130570215688563,6,reviewed,uw,uw
2022-01-22T14:32:21.935Z,61.67,-148.0841,17.4,1.5,ml,,,,0.6,ak,ak02210mclxt,2022-01-22T14:35:53.394Z,"24 km SE of Chickaloon, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-22T14:21:39.150Z,18.8275,-64.6493,23,3.59,md,18,319,1.1615,0.3,pr,pr2022022005,2022-01-22T17:49:42.040Z,"56 km NNE of Cruz Bay, U.S. Virgin Islands",earthquake,1.75,22.91,0.06,17,reviewed,pr,pr
2022-01-22T14:18:35.237Z,59.7914,-153.2864,132.6,1.7,ml,,,,0.61,ak,ak02210m9mzj,2022-01-22T14:21:11.670Z,"46 km E of Pedro Bay, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-22T14:16:10.420Z,19.1695003509521,-155.502166748047,32.1599998474121,1.75999999,md,26,154,,0.129999995,hv,hv72885917,2022-01-22T14:19:28.760Z,"4 km SW of Pāhala, Hawaii",earthquake,0.61,1.51999998,1.75999999,4,automatic,hv,hv
2022-01-22T14:12:03.520Z,19.2264995574951,-155.456665039062,30.6200008392334,2.16000009,md,42,106,,0.109999999,hv,hv72885912,2022-01-22T14:15:19.720Z,"3 km NE of Pāhala, Hawaii",earthquake,0.47,0.610000014,0.699999988,20,automatic,hv,hv
2022-01-22T13:49:49.880Z,2.8166,127.4791,61.67,4.9,mb,,87,2.034,1.03,us,us7000ge7m,2022-01-22T14:11:13.040Z,"134 km NNW of Tobelo, Indonesia",earthquake,7.2,7.9,0.064,78,reviewed,us,us
2022-01-22T13:49:13.500Z,38.7970009,-122.7338333,1.11,0.87,md,6,208,0.01393,0.01,nc,nc73681966,2022-01-22T13:50:48.478Z,"3km NE of The Geysers, CA",earthquake,0.67,1.09,,1,automatic,nc,nc
2022-01-22T13:41:30.530Z,35.1515,-118.1933333,7.11,1.4,ml,26,64,0.1449,0.2,ci,ci39920415,2022-01-22T13:52:28.650Z,"11km N of Mojave, CA",earthquake,0.37,1.34,0.137,28,automatic,ci,ci
2022-01-22T13:38:35.820Z,19.2329998016357,-155.452667236328,29.7299995422363,1.97000003,md,39,107,,0.109999999,hv,hv72885877,2022-01-22T13:41:40.330Z,"4 km NE of Pāhala, Hawaii",earthquake,0.48,0.680000007,0.699999988,13,automatic,hv,hv
2022-01-22T13:20:34.030Z,19.1926670074463,-155.475173950195,35.1100006103516,2.18,ml,46,87,,0.119999997,hv,hv72885862,2022-01-22T16:47:30.040Z,"1 km SSE of Pāhala, Hawaii",earthquake,0.57,0.74000001,4.4,9,automatic,hv,hv
2022-01-22T13:19:43.710Z,35.0528333,-118.375,10.11,1.3,ml,12,79,0.06788,0.15,ci,ci39920375,2022-01-22T13:23:24.850Z,"11km SE of Tehachapi, CA",earthquake,0.35,0.73,0.267,28,automatic,ci,ci
2022-01-22T13:16:16.330Z,19.2063331604004,-155.432998657227,33.8899993896484,1.85000002,md,37,135,,0.109999999,hv,hv72885857,2022-01-22T13:19:30.080Z,"4 km E of Pāhala, Hawaii",earthquake,0.57,0.689999998,1.05999994,8,automatic,hv,hv
2022-01-22T12:59:57.060Z,19.1996669769287,-155.403335571289,32.8899993896484,2.1400001,md,40,158,,0.140000001,hv,hv72885852,2022-01-22T13:12:33.730Z,"7 km E of Pāhala, Hawaii",earthquake,0.54,0.800000012,0.800000012,16,automatic,hv,hv
2022-01-22T12:53:43.990Z,34.222,-117.4731667,6.69,1.68,ml,42,51,0.08936,0.19,ci,ci39920359,2022-01-22T12:57:29.747Z,"5km SSE of Lytle Creek, CA",earthquake,0.23,0.74,0.146,26,automatic,ci,ci
2022-01-22T12:37:41.500Z,37.3198333,-122.1438333,4.28,1.16,md,17,78,0.007524,0.18,nc,nc73681956,2022-01-22T21:47:11.957Z,"5km SW of Loyola, CA",earthquake,0.37,0.57,0.081,13,reviewed,nc,nc
2022-01-22T12:23:41.480Z,37.4953333,-118.8523333,4.32,0.6,md,15,125,0.09631,0.03,nc,nc73681951,2022-01-22T16:55:34.876Z,"17km WSW of Toms Place, CA",earthquake,0.54,1.31,0.198,13,reviewed,nc,nc
2022-01-22T12:22:31.650Z,36.9855003,-121.6428299,4.05,1.34,md,9,53,0.05624,0.07,nc,nc73681946,2022-01-22T12:54:10.836Z,"7km WSW of Gilroy, CA",earthquake,0.34,0.95,0.29,9,automatic,nc,nc
2022-01-22T12:04:30.780Z,19.1875,-155.475997924805,35.7299995422363,1.77999997,md,36,84,,0.129999995,hv,hv72885817,2022-01-22T12:07:49.940Z,"1 km S of Pāhala, Hawaii",earthquake,0.61,1.12,0.25,5,automatic,hv,hv
2022-01-22T12:04:01.201Z,61.1503,-150.705,32.7,1.7,ml,,,,0.45,ak,ak02210kzp2w,2022-01-22T12:10:48.210Z,"20 km E of Beluga, Alaska",earthquake,,2.7,,,automatic,ak,ak
2022-01-22T11:46:38.250Z,37.4898333,-118.859,3.79,0.45,md,8,127,0.1028,0.11,nc,nc73681941,2022-01-22T16:48:35.041Z,"18km WSW of Toms Place, CA",earthquake,0.86,4.13,0.262,8,reviewed,nc,nc
2022-01-22T11:30:15.190Z,19.1881675720215,-155.475662231445,34.9599990844727,2.04999995,md,38,85,,0.129999995,hv,hv72885767,2022-01-22T11:33:35.750Z,"1 km S of Pāhala, Hawaii",earthquake,0.66,0.829999983,0.170000002,9,automatic,hv,hv
2022-01-22T11:29:16.280Z,61.5947,-149.9267,32.7,1.9,ml,,,,0.38,ak,ak02210kjnjg,2022-01-22T11:33:44.016Z,"6 km SW of Houston, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-22T11:10:10.954Z,59.6088,-152.4522,76.7,1.6,ml,,,,0.23,ak,ak02210kfke3,2022-01-22T11:17:22.065Z,"39 km WSW of Anchor Point, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-22T11:09:33.695Z,-20.6585,-175.4862,10,4.6,mb,,124,6.757,0.42,us,us7000gea1,2022-01-22T22:16:17.040Z,"60 km NNW of Nuku‘alofa, Tonga",earthquake,14,1.9,0.112,24,reviewed,us,us
2022-01-22T10:43:14.320Z,33.0331667,-115.6053333,4.2,1.29,ml,10,128,0.02032,0.24,ci,ci39920343,2022-01-22T10:46:43.983Z,"2km ESE of Westmorland, CA",earthquake,0.85,0.79,0.232,16,automatic,ci,ci
2022-01-22T10:33:42.360Z,19.007,-66.7516,36,3.47,md,16,260,0.5746,0.36,pr,pr2022022003,2022-01-22T11:05:42.907Z,"58 km N of Hatillo, Puerto Rico",earthquake,1.32,5.24,0.07,9,reviewed,pr,pr
2022-01-22T10:25:57.272Z,57.1094,-154.6887,35,2.7,ml,,261,0.475,0.15,us,us7000ge74,2022-01-22T10:54:02.040Z,"36 km WNW of Akhiok, Alaska",earthquake,6.1,2,0.063,33,reviewed,us,us
2022-01-22T10:24:47.270Z,17.8965,-66.834,12,2.17,md,4,318,0.0907,0.02,pr,pr2022022004,2022-01-22T11:10:35.490Z,"10 km SSE of Maria Antonia, Puerto Rico",earthquake,0.76,0.92,0.12,4,reviewed,pr,pr
2022-01-22T10:17:58.220Z,19.2280006408691,-155.460494995117,34.5,2.36,ml,46,103,,0.129999995,hv,hv72885692,2022-01-22T10:46:05.040Z,"3 km NE of Pāhala, Hawaii",earthquake,0.45,0.639999986,4.16,11,automatic,hv,hv
2022-01-22T10:17:06.830Z,35.972332,-119.7438354,9.21,2.09,md,13,111,0.3116,0.12,nc,nc73681921,2022-01-22T10:42:11.073Z,"20km ESE of Kettleman City, CA",earthquake,0.6,2.35,0.03,5,automatic,nc,nc
2022-01-22T09:41:39.960Z,38.8919983,-122.8335037,2.14,1.53,md,9,187,0.02208,0.03,nc,nc73681906,2022-01-22T10:27:09.980Z,"10km S of Kelseyville, CA",earthquake,0.64,0.83,0.09,3,automatic,nc,nc
2022-01-22T09:24:07.870Z,33.9941667,-118.3505,7.93,1.5,ml,24,56,0.009995,0.31,ci,ci39920319,2022-01-22T11:29:35.600Z,"0km SW of View Park-Windsor Hills, CA",earthquake,0.51,0.61,0.245,29,automatic,ci,ci
2022-01-22T09:23:40.075Z,-18.0417,-173.5175,35,4.8,mb,,72,8.031,0.58,us,us7000ge70,2022-01-22T10:02:47.040Z,"83 km NE of Neiafu, Tonga",earthquake,6.4,2,0.043,178,reviewed,us,us
2022-01-22T09:22:01.990Z,38.8370018,-122.8078308,2.2,1.18,md,9,88,0.0137,0.01,nc,nc73681896,2022-01-22T10:02:10.798Z,"8km WNW of Cobb, CA",earthquake,0.42,1.38,,1,automatic,nc,nc
2022-01-22T09:05:51.950Z,45.8686666666667,-122.253,6.12,1.36,ml,19,116,0.1325,0.26,uw,uw61812231,2022-01-23T05:45:02.580Z,"11 km E of Yacolt, Washington",earthquake,0.65,1.7,0.152874825469723,11,reviewed,uw,uw
2022-01-22T09:01:33.186Z,3.6218,126.701,59.41,4.5,mb,,109,2.908,0.46,us,us7000ge6y,2022-01-22T09:36:40.040Z,"240 km SE of Sarangani, Philippines",earthquake,8.1,8.2,0.095,37,reviewed,us,us
2022-01-22T08:50:16.160Z,33.4791667,-116.4318333,12.4,1.09,ml,31,78,0.1139,0.19,ci,ci39920303,2022-01-22T16:47:55.610Z,"23km SSW of La Quinta, CA",earthquake,0.31,0.63,0.153,26,reviewed,ci,ci
2022-01-22T08:11:51.865Z,63.8872,-147.2246,7.2,2.9,ml,,,,0.8,ak,ak02210inkhk,2022-01-22T09:21:56.040Z,"61 km SSW of Harding-Birch Lakes, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-22T07:57:39.310Z,38.8181648,-122.8218307,3.12,0.85,md,10,93,0.01056,0.02,nc,nc73681891,2022-01-22T07:59:12.633Z,"7km NW of The Geysers, CA",earthquake,0.4,1.63,,1,automatic,nc,nc
2022-01-22T07:54:45.820Z,38.8445015,-122.8303299,2.01,1.19,md,14,121,0.007147,0.02,nc,nc73681886,2022-01-22T09:15:12.506Z,"10km WNW of Cobb, CA",earthquake,0.31,0.67,,1,automatic,nc,nc
2022-01-22T07:49:37.220Z,19.1908340454102,-155.489334106445,36.3300018310547,2.28999996,md,38,76,,0.119999997,hv,hv72885572,2022-01-22T07:52:46.370Z,"1 km SW of Pāhala, Hawaii",earthquake,0.54,0.839999974,0.479999989,13,automatic,hv,hv
2022-01-22T07:46:15.568Z,54.5273,-163.2739,10,2.9,ml,,190,0.34,0.56,us,us7000ge8z,2022-01-23T06:17:10.040Z,"37 km SSE of False Pass, Alaska",earthquake,3.3,2,0.101,13,reviewed,us,us
2022-01-22T07:45:54.650Z,53.1716,-166.7875,25.8,2.2,ml,,,,0.35,ak,ak02210i9fjd,2022-01-22T19:10:04.441Z,"79 km SSW of Unalaska, Alaska",earthquake,,172,,,reviewed,ak,ak
2022-01-22T07:42:33.850Z,38.7876663,-122.7344971,1.12,1.33,md,12,88,0.004753,0.04,nc,nc73681881,2022-01-22T08:48:21.363Z,"2km ENE of The Geysers, CA",earthquake,0.32,0.43,0.16,4,automatic,nc,nc
2022-01-22T07:33:16.260Z,38.7878342,-122.7665024,2.44,1.08,md,13,79,0.01383,0.02,nc,nc73681876,2022-01-22T07:39:38.687Z,"2km NW of The Geysers, CA",earthquake,0.35,0.73,0.11,2,automatic,nc,nc
2022-01-22T07:31:58.820Z,44.4631667,-115.2046667,4.94,1.74,ml,8,117,0.843,0.19,mb,mb80536604,2022-01-22T16:00:13.650Z,"34 km NW of Stanley, Idaho",earthquake,0.68,1.53,0.235,9,reviewed,mb,mb
2022-01-22T07:30:04.478Z,60.6966,-151.6711,76.9,1.5,ml,,,,0.25,ak,ak02210i63xg,2022-01-22T07:34:38.391Z,"20 km W of Nikiski, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-22T07:25:34.570Z,19.1378326416016,-155.495834350586,32.1199989318848,1.91999996,md,32,165,,0.189999998,hv,hv72885542,2022-01-22T07:28:49.980Z,"7 km SSW of Pāhala, Hawaii",earthquake,0.7,1.13,0.899999976,7,automatic,hv,hv
2022-01-22T07:24:11.840Z,38.8296661,-122.7961655,0.82,1.17,md,8,91,0.009843,0.01,nc,nc73681871,2022-01-22T08:22:12.219Z,"6km W of Cobb, CA",earthquake,0.32,1.04,,1,automatic,nc,nc
2022-01-22T07:23:47.520Z,38.8278351,-122.796669,0.76,1.53,md,26,44,0.01137,0.04,nc,nc73681866,2022-01-22T07:53:12.055Z,"6km W of Cobb, CA",earthquake,0.17,0.34,0.14,7,automatic,nc,nc
2022-01-22T07:23:34.227Z,-14.5242,-75.5338,48.3,4.8,mb,,148,6.28,0.67,us,us7000ge6j,2022-01-22T07:54:37.321Z,"35 km W of Llipata, Peru",earthquake,9.3,7.9,0.074,57,reviewed,us,us
2022-01-22T07:08:10.916Z,3.6286,126.6284,10,4.9,mb,,103,2.932,0.5,us,us7000ge6i,2022-01-22T07:33:47.040Z,"234 km SSE of Sarangani, Philippines",earthquake,5.1,1.9,0.096,34,reviewed,us,us
2022-01-22T06:59:38.817Z,62.9657,-149.2594,75.5,1.9,ml,,,,0.62,ak,ak02210hqyqn,2022-01-22T07:04:45.030Z,"49 km SSW of Cantwell, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-22T06:30:16.704Z,-1.7716,-12.9571,10,4.9,mb,,48,6.278,0.61,us,us7000ge6e,2022-01-22T07:00:18.040Z,"north of Ascension Island",earthquake,9.8,1.9,0.096,34,reviewed,us,us
2022-01-22T06:28:56.360Z,35.9749985,-119.7416687,6.9,2.12,md,15,111,0.3109,0.08,nc,nc73681851,2022-01-22T07:24:10.872Z,"20km E of Kettleman City, CA",earthquake,0.37,1.19,0.12,6,automatic,nc,nc
2022-01-22T06:23:52.420Z,19.166166305542,-155.486999511719,34.8699989318848,2.17000008,md,36,104,,0.129999995,hv,hv72885502,2022-01-22T06:28:47.450Z,"4 km SSW of Pāhala, Hawaii",earthquake,0.5,0.889999986,0.850000024,9,automatic,hv,hv
2022-01-22T06:18:48.386Z,62.9658,-150.2876,54.4,2.3,ml,,,,0.89,ak,ak02210hi6yy,2022-01-22T06:25:20.822Z,"57 km NNE of Petersville, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-22T06:15:20.430Z,33.5146667,-116.4893333,15.22,0.95,ml,15,68,0.0551,0.15,ci,ci39920271,2022-01-22T16:47:58.785Z,"18km ESE of Anza, CA",earthquake,0.4,0.49,0.254,23,reviewed,ci,ci
2022-01-22T06:13:10.580Z,35.6650009,-120.1743317,1.96,1.83,md,7,170,0.08984,0.06,nc,nc73681841,2022-01-22T07:08:11.773Z,"13km ESE of Cholame, CA",earthquake,2.14,7.7,0.01,2,automatic,nc,nc
2022-01-22T06:01:38.540Z,38.7901667,-122.7615,2.19,0.58,md,13,94,0.01054,0.04,nc,nc73681836,2022-01-22T22:20:31.747Z,"2km NNW of The Geysers, CA",earthquake,0.35,0.62,,1,reviewed,nc,nc
2022-01-22T05:49:37.245Z,29.3909,142.3725,10,4.9,mb,,125,4.31,0.6,us,us7000ge62,2022-01-22T11:00:33.170Z,"Izu Islands, Japan region",earthquake,10.3,1.9,0.081,48,reviewed,us,us
2022-01-22T05:43:24.090Z,38.8218346,-122.8050003,2.6,0.88,md,16,70,0.004259,0.02,nc,nc73681826,2022-01-22T05:44:59.012Z,"6km NW of The Geysers, CA",earthquake,0.27,0.57,0.29,3,automatic,nc,nc
2022-01-22T05:38:48.126Z,53.177,-166.7508,25.86,3.9,mb,,166,0.622,0.83,us,us7000ge67,2022-01-22T06:19:44.040Z,"78 km S of Unalaska, Alaska",earthquake,4,7.1,0.092,31,reviewed,us,us
2022-01-22T05:37:02.350Z,35.9286652,-119.8608322,4.27,2.01,md,8,181,0.2668,0.2,nc,nc73681821,2022-01-22T06:43:10.638Z,"13km SE of Kettleman City, CA",earthquake,3.04,10.36,0.14,4,automatic,nc,nc
2022-01-22T05:33:31.330Z,33.2495,-117.4351667,15.69,1.12,ml,13,225,0.07,0.1,ci,ci39920231,2022-01-22T05:37:09.443Z,"6km WNW of Camp Pendleton South, CA",earthquake,0.38,0.35,0.116,18,automatic,ci,ci
2022-01-22T05:32:30.740Z,33.645,-116.703,13.22,1.25,ml,34,51,0.06665,0.17,ci,ci39920223,2022-01-22T16:49:10.530Z,"10km NNW of Anza, CA",earthquake,0.27,0.43,0.198,27,reviewed,ci,ci
2022-01-22T05:26:06.730Z,19.2258338928223,-155.417663574219,31.5300006866455,2.55,ml,42,134,,0.200000003,hv,hv72885447,2022-01-22T05:39:21.040Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.55,0.930000007,0.24,5,automatic,hv,hv
2022-01-22T05:25:54.500Z,19.1973323822021,-155.466659545898,32.8699989318848,2.58,ml,19,203,,0.180000007,hv,hv72885452,2022-01-22T05:31:44.870Z,"1 km ESE of Pāhala, Hawaii",earthquake,1.77,1.08000004,4.62,6,automatic,hv,hv
2022-01-22T05:20:17.820Z,19.2153339385986,-155.458999633789,34.4799995422363,2.01999998,md,34,106,,0.129999995,hv,hv72885442,2022-01-22T05:23:22.740Z,"2 km ENE of Pāhala, Hawaii",earthquake,0.57,0.720000029,0.319999993,13,automatic,hv,hv
2022-01-22T05:19:05.102Z,53.2115,-166.8168,43.35,4.6,ml,,216,0.584,0.51,us,us7000ge64,2022-01-22T06:15:23.040Z,"76 km SSW of Unalaska, Alaska",earthquake,8,37.4,0.105,12,reviewed,us,us
2022-01-22T05:17:53.790Z,35.9491653,-119.7508316,19.81,2.12,md,10,143,0.3313,0.04,nc,nc73681806,2022-01-22T06:04:10.399Z,"20km ESE of Kettleman City, CA",earthquake,1.53,0.87,0.03,2,automatic,nc,nc
2022-01-22T05:17:06.947Z,53.3159,-166.7506,42.78,6.2,mww,,60,0.484,1.44,us,us7000ge5q,2022-01-23T05:27:18.185Z,"63 km SSW of Unalaska, Alaska",earthquake,6.1,4.6,0.034,82,reviewed,us,us
2022-01-22T05:13:59.870Z,33.8188333,-117.6438333,5.57,1.32,ml,26,34,0.03727,0.23,ci,ci39920215,2022-01-22T05:17:42.556Z,"9km SW of Corona, CA",earthquake,0.33,0.56,0.216,32,automatic,ci,ci
2022-01-22T05:12:33.846Z,-20.7797,-175.3928,10,4.7,mb,,124,6.887,0.65,us,us7000ge5z,2022-01-22T05:50:31.040Z,"44 km NNW of Nuku‘alofa, Tonga",earthquake,9.2,1.9,0.207,7,reviewed,us,us
2022-01-22T04:59:59.520Z,38.8364983,-122.8184967,1.88,0.85,md,9,160,0.01343,0.02,nc,nc73681801,2022-01-22T05:01:38.331Z,"8km W of Cobb, CA",earthquake,0.68,0.84,,1,automatic,nc,nc
2022-01-22T04:59:05.340Z,19.2313327789307,-155.462326049805,33.9900016784668,2.27999997,md,34,99,,0.140000001,hv,hv72885432,2022-01-22T05:04:36.400Z,"3 km NNE of Pāhala, Hawaii",earthquake,0.78,0.930000007,1.12,12,automatic,hv,hv
2022-01-22T04:56:11.160Z,38.8343315,-122.8156662,0.63,1.58,md,16,58,0.01176,0.06,nc,nc73681796,2022-01-22T05:48:13.293Z,"8km W of Cobb, CA",earthquake,0.26,0.55,0.03,3,automatic,nc,nc
2022-01-22T04:46:20.010Z,18.0201,-66.7683,13,2.91,md,17,78,0.1197,0.12,pr,pr2022022002,2022-01-22T15:13:44.616Z,"0 km NNE of Magas Arriba, Puerto Rico",earthquake,0.4,0.17,0.19,4,reviewed,pr,pr
2022-01-22T04:41:05.502Z,-59.4138,-25.894,35,5.1,mww,,69,7.751,1.03,us,us7000ge5f,2022-01-22T17:21:56.040Z,"South Sandwich Islands region",earthquake,11,1.9,0.098,10,reviewed,us,us
2022-01-22T04:31:50.810Z,33.6558333,-116.7143333,15.66,0.88,ml,29,57,0.05519,0.17,ci,ci39920199,2022-01-22T04:35:26.731Z,"9km S of Idyllwild, CA",earthquake,0.27,0.43,0.175,23,automatic,ci,ci
2022-01-22T04:20:54.062Z,32.7191,132.0414,52.31,4.4,mb,,99,1.809,1.01,us,us7000ge59,2022-01-22T04:40:47.040Z,"28 km SSE of Saiki, Japan",earthquake,6.5,7.7,0.22,8,reviewed,us,us
2022-01-22T04:11:18.610Z,34.0231667,-117.1106667,13.43,1.02,ml,22,82,0.01236,0.17,ci,ci39920183,2022-01-22T04:14:57.396Z,"6km SSE of Mentone, CA",earthquake,0.34,0.82,0.167,29,automatic,ci,ci
2022-01-22T04:05:49.686Z,43.3503,145.7905,111.64,4.2,mb,,197,2.355,0.48,us,us7000ge51,2022-01-22T04:24:11.040Z,"17 km E of Nemuro, Japan",earthquake,7.9,11.6,0.166,11,reviewed,us,us
2022-01-22T04:04:41.780Z,40.6123333,-122.1655,12.65,1.3,md,6,108,0.03377,0.05,nc,nc73681786,2022-01-22T17:14:11.476Z,"6km ESE of Bella Vista, CA",earthquake,0.47,0.43,0.25,5,reviewed,nc,nc
2022-01-22T03:52:02.410Z,34.0343323,-117.1973343,18.06,1.32,ml,23,105,0.1535,0.22,ci,ci39920167,2022-01-22T03:55:38.470Z,"3km SSW of Redlands, CA",earthquake,0.48,1.16,0.221,4,automatic,ci,ci
2022-01-22T03:34:00.170Z,37.5116667,-118.8565,2.85,0.21,md,8,321,0.0812,0.01,nc,nc73681776,2022-01-22T16:38:03.317Z,"16km WSW of Toms Place, CA",earthquake,1.4,1.61,0.085,7,reviewed,nc,nc
2022-01-22T03:24:39.805Z,63.0184,-150.6151,103,2.4,ml,,,,0.6,ak,ak02210fr5wb,2022-01-22T03:38:22.374Z,"58 km N of Petersville, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-22T03:18:17.190Z,61.8308,-151.13,65.4,1.8,ml,,,,0.75,ak,ak02210fptwc,2022-01-22T03:22:50.367Z,"22 km SE of Skwentna, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-22T02:46:52.180Z,19.482666015625,-155.454498291016,0,1.76999998,md,14,63,,0.209999993,hv,hv72885302,2022-01-22T02:50:05.750Z,"23 km W of Volcano, Hawaii",earthquake,0.4,1.09000003,0.879999995,3,automatic,hv,hv
2022-01-22T02:46:49.270Z,33.1641667,-116.441,11.96,1.11,ml,30,60,0.1057,0.22,ci,ci39920119,2022-01-22T02:57:26.280Z,"12km SSW of Borrego Springs, CA",earthquake,0.31,0.83,0.218,28,automatic,ci,ci
2022-01-22T02:46:15.393Z,63.0791,-150.3496,87.6,1.5,ml,,,,0.41,ak,ak02210fae0r,2022-01-22T02:50:07.021Z,"68 km NNE of Petersville, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-22T02:42:26.600Z,37.3751678,-121.4520035,6.26,1.2,md,9,107,0.07106,0.07,nc,nc73681771,2022-01-22T04:20:11.247Z,"29km SW of Westley, CA",earthquake,0.41,1.39,0.04,7,automatic,nc,nc
2022-01-22T02:26:13.573Z,3.6951,126.6747,23.99,6,mww,,34,2.985,0.98,us,us7000ge38,2022-01-23T02:31:01.849Z,"231 km SE of Sarangani, Philippines",earthquake,6.8,4.2,0.052,36,reviewed,us,us
2022-01-22T02:20:32.640Z,38.815,-122.761,2.23,0.58,md,27,61,0.01439,0.03,nc,nc73681766,2022-01-22T22:12:01.454Z,"3km WSW of Cobb, CA",earthquake,0.22,0.31,0.106,3,reviewed,nc,nc
2022-01-22T02:20:20.390Z,19.8395004272461,-155.359664916992,30.1499996185303,2.18000007,md,25,137,,0.150000006,hv,hv72885272,2022-01-22T02:23:19.850Z,"20 km SW of Laupāhoehoe, Hawaii",earthquake,0.82,1.37,1.08000004,3,automatic,hv,hv
2022-01-22T02:10:36.870Z,19.0515,-65.36,34,3.62,md,16,291,0.748,0.4,pr,pr2022022001,2022-01-22T03:03:46.350Z,"83 km N of Culebra, Puerto Rico",earthquake,3.06,15.15,0.12,4,reviewed,pr,pr
2022-01-22T01:54:41.810Z,19.2124996185303,-155.417999267578,33.2200012207031,2.07999992,md,37,143,,0.119999997,hv,hv72885257,2022-01-22T01:57:52.220Z,"6 km E of Pāhala, Hawaii",earthquake,0.71,1.08000004,1.41999996,20,automatic,hv,hv
2022-01-22T01:48:17.879Z,64.6148,-152.2349,0,2.2,ml,,,,1.08,ak,ak02210epebg,2022-01-22T01:57:21.344Z,"62 km S of Tanana, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-22T01:45:18.320Z,38.7896652,-122.7628326,0.49,1.42,md,22,66,0.01121,0.06,nc,nc73681761,2022-01-22T03:27:10.981Z,"2km NNW of The Geysers, CA",earthquake,0.23,0.38,0.08,6,automatic,nc,nc
2022-01-22T01:41:55.620Z,19.1508333333333,-155.471666666667,33.46,2.73,md,48,161,,0.12,hv,hv72885237,2022-01-22T05:33:13.040Z,"5 km S of Pāhala, Hawaii",earthquake,0.47,0.6,0.0819856873128886,20,reviewed,hv,hv
2022-01-22T01:35:32.350Z,37.3336667,-118.1523333,12.23,1.53,md,12,241,0.143,0.06,nc,nc73681751,2022-01-22T22:14:11.125Z,"16km WSW of Deep Springs, CA",earthquake,0.55,0.62,0.316,10,reviewed,nc,nc
2022-01-22T01:28:49.166Z,59.2578,-154.6778,0,2.2,ml,,,,0.72,ak,ak02210el6b8,2022-01-22T01:48:57.040Z,"20 km SSE of Kokhanok, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-22T01:05:09.810Z,19.0821,-65.3633,12,3.4,md,12,292,0.7788,0.19,pr,pr2022022000,2022-01-22T02:07:31.159Z,"86 km N of Culebra, Puerto Rico",earthquake,5.68,7.37,0.07,3,reviewed,pr,pr
2022-01-22T01:01:42.300Z,32.8625,-116.0805,7.23,3.01,ml,92,31,0.07185,0.22,ci,ci39920079,2022-01-23T02:30:01.450Z,"16km NNW of Ocotillo, CA",earthquake,0.14,0.53,0.193,113,reviewed,ci,ci
2022-01-22T01:01:00.990Z,38.8310013,-122.8190002,1.52,0.85,md,12,65,0.01031,0.02,nc,nc73681736,2022-01-22T01:02:37.518Z,"8km NW of The Geysers, CA",earthquake,0.28,0.7,,1,automatic,nc,nc
2022-01-22T00:53:43.980Z,37.2033348,-121.5944977,3.61,1.38,md,12,65,0.04728,0.08,nc,nc73681731,2022-01-22T01:51:12.152Z,"10km NNE of Morgan Hill, CA",earthquake,0.31,0.82,0.16,11,automatic,nc,nc
2022-01-22T00:53:32.190Z,38.8344994,-122.8160019,1.67,0.36,md,9,76,0.01202,0,nc,nc73681726,2022-01-22T00:55:07.288Z,"8km W of Cobb, CA",earthquake,0.41,1.6,,1,automatic,nc,nc
2022-01-22T00:45:38.850Z,33.9153333,-117.8988333,3.61,1.35,ml,30,89,0.03643,0.33,ci,ci39920071,2022-01-22T00:54:41.472Z,"0km SE of Brea, CA",earthquake,0.57,0.54,0.235,30,automatic,ci,ci
2022-01-22T00:42:51.334Z,61.7532,-149.5498,54.3,1.7,ml,,,,0.8,ak,ak02210e2qwd,2022-01-22T00:46:23.573Z,"14 km N of Meadow Lakes, Alaska",earthquake,,1.9,,,automatic,ak,ak
2022-01-22T00:33:31.250Z,40.3193321,-124.229332,23.42,1.91,md,9,126,0.04211,0.05,nc,nc73681716,2022-01-22T00:44:10.653Z,"5km E of Petrolia, CA",earthquake,1.19,1.23,0.17,4,automatic,nc,nc
2022-01-22T00:23:20.000Z,34.0031667,-116.8155,13.06,1.65,ml,44,53,0.03254,0.2,ci,ci39920063,2022-01-22T00:34:39.680Z,"10km NNW of Cabazon, CA",earthquake,0.32,0.66,0.144,27,automatic,ci,ci
2022-01-22T00:17:44.220Z,38.8121681,-122.7573318,0.6,1.2,md,14,176,0.01168,0.02,nc,nc73681706,2022-01-22T00:39:11.623Z,"3km WSW of Cobb, CA",earthquake,0.31,0.47,0.22,2,automatic,nc,nc
2022-01-22T00:03:19.426Z,64.9675,-147.4566,0,1.6,ml,,,,0.84,ak,ak02210dubcp,2022-01-22T00:46:23.428Z,"7 km E of Fox, Alaska",explosion,,1.5,,,automatic,ak,ak
2022-01-22T00:00:16.870Z,34.007,-118.3478333,7.03,1.22,ml,17,71,0.02007,0.2,ci,ci39920039,2022-01-22T01:14:15.877Z,"1km N of View Park-Windsor Hills, CA",earthquake,0.38,0.56,0.225,13,reviewed,ci,ci
2022-01-21T23:56:14.580Z,37.7288322,-121.9921646,5.79,2.11,md,12,102,0.05834,0.09,nc,nc73681691,2022-01-22T14:23:39.449Z,"6km WNW of Dublin, CA",earthquake,0.4,0.83,0.19,10,automatic,nc,nc
2022-01-21T23:54:28.708Z,-21.8503,-177.8219,371.18,4.3,mb,,166,5.635,0.85,us,us7000ge2f,2022-01-22T01:03:37.040Z,"281 km WSW of Haveluloto, Tonga",earthquake,10.6,8.3,0.119,20,reviewed,us,us
2022-01-21T23:54:11.692Z,38.4957,-119.3927,0,1.6,ml,9,98.32,0.037,0.1519,nn,nn00832165,2022-01-22T02:37:21.059Z,"7 km ESE of Walker, California",earthquake,,0,0.34,5,reviewed,nn,nn
2022-01-21T23:49:05.665Z,61.5379,-149.7403,33.5,1.6,ml,,,,0.36,ak,ak022z49rt2,2022-01-21T23:52:17.848Z,"7 km WNW of Knik-Fairview, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-21T23:43:37.019Z,59.7805,-151.9982,50.3,1.8,ml,,,,1.05,ak,ak022z48jxc,2022-01-21T23:48:37.323Z,"9 km W of Anchor Point, Alaska",earthquake,,2.1,,,automatic,ak,ak
2022-01-21T23:41:08.700Z,37.7271652,-121.9925003,5.64,2.21,md,15,102,0.05836,0.08,nc,nc73681681,2022-01-22T14:28:49.435Z,"6km WNW of Dublin, CA",earthquake,0.33,0.73,0.16,11,automatic,nc,nc
2022-01-21T23:37:54.970Z,37.9211655,-122.1231689,4.43,1.6,md,11,83,0.02342,0.08,nc,nc73681676,2022-01-22T07:18:44.631Z,"4km N of Lafayette, CA",earthquake,0.34,0.72,0.21,9,automatic,nc,nc
2022-01-21T23:36:11.060Z,19.2103328704834,-155.413497924805,30.6800003051758,1.87,md,29,153,,0.119999997,hv,hv72885127,2022-01-21T23:39:34.650Z,"6 km E of Pāhala, Hawaii",earthquake,0.7,1.21000004,0.99000001,7,automatic,hv,hv
2022-01-21T23:35:26.270Z,37.4891667,-118.8213333,2.47,0.33,md,7,271,0.09702,0.1,nc,nc73681671,2022-01-22T21:15:26.948Z,"15km WSW of Toms Place, CA",earthquake,1.45,5.95,0.255,6,reviewed,nc,nc
2022-01-21T23:32:56.030Z,38.7501678,-122.7220001,0.99,1.59,md,13,186,0.01163,0.02,nc,nc73681666,2022-01-21T23:51:11.545Z,"4km SW of Anderson Springs, CA",earthquake,0.44,0.31,0.22,3,automatic,nc,nc
2022-01-21T23:31:08.680Z,19.2250003814697,-155.411499023438,32.9700012207031,2.07,ml,43,138,,0.129999995,hv,hv72885122,2022-01-21T23:55:23.040Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.51,0.670000017,3.37,7,automatic,hv,hv
2022-01-21T23:29:07.520Z,38.7578316,-122.7176666,1.49,0.39,md,6,160,0.006763,0.01,nc,nc73681661,2022-01-21T23:30:41.059Z,"3km SW of Anderson Springs, CA",earthquake,0.71,0.57,,1,automatic,nc,nc
2022-01-21T23:24:26.941Z,62.3954,-151.5495,85.5,2,ml,,,,0.85,ak,ak022z44gjq,2022-01-21T23:32:45.459Z,"42 km WSW of Petersville, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-21T23:20:14.530Z,38.1542,-117.906,9.4,1.2,ml,16,107.79,0.045,0.1496,nn,nn00832160,2022-01-22T00:47:36.541Z,"31 km SE of Mina, Nevada",earthquake,,1.1,0.46,6,reviewed,nn,nn
2022-01-21T23:18:01.170Z,39.4175,-110.298,-3.12,1.43,md,7,200,0.022,0.11,uu,uu60478487,2022-01-21T23:46:11.920Z,"16 km SSE of Sunnyside, Utah",earthquake,0.68,1.53,0.282,7,reviewed,uu,uu
2022-01-21T23:13:05.530Z,35.0045,-118.1826667,-0.86,1.57,ml,10,82,0.1309,0.25,ci,ci39920007,2022-01-21T23:49:46.464Z,"5km S of Mojave, CA",quarry blast,0.79,31.61,0.272,13,reviewed,ci,ci
2022-01-21T23:05:47.520Z,38.8251648,-122.7639999,0.38,0.85,md,8,127,0.007029,0.02,nc,nc73681656,2022-01-21T23:07:21.597Z,"4km W of Cobb, CA",earthquake,0.42,0.94,,1,automatic,nc,nc
2022-01-21T23:01:48.353Z,38.405,-118.9018,9.2,1.3,ml,13,167.3,0.119,0.1215,nn,nn00832170,2022-01-22T02:37:28.336Z,"27 km WSW of Hawthorne, Nevada",earthquake,,2.1,0.32,4,reviewed,nn,nn
2022-01-21T22:49:20.890Z,39.4166667,-110.3113333,-1.45,1.79,md,5,196,0.01299,0.05,uu,uu60478482,2022-01-21T23:41:01.510Z,"16 km SSE of Sunnyside, Utah",earthquake,0.75,0.48,0.286,5,reviewed,uu,uu
2022-01-21T22:49:01.337Z,54.3147,158.5376,162.66,4.4,mb,,107,1.295,0.53,us,us7000ge1v,2022-01-21T23:15:01.040Z,"42 km S of Mil’kovo, Russia",earthquake,10.2,8.9,0.084,41,reviewed,us,us
2022-01-21T22:47:11.490Z,19.2360000610352,-155.430999755859,33.5900001525879,2.26999998,md,39,121,,0.109999999,hv,hv72885092,2022-01-21T22:50:22.340Z,"6 km NE of Pāhala, Hawaii",earthquake,0.67,0.839999974,0.150000006,20,automatic,hv,hv
2022-01-21T22:42:27.810Z,19.4093333333333,-155.271666666667,2.75,1.67,ml,16,76,,0.11,hv,hv72885087,2022-01-21T22:56:41.730Z,"5 km SW of Volcano, Hawaii",earthquake,0.22,0.32,0.273255795376414,8,reviewed,hv,hv
2022-01-21T22:20:40.190Z,59.6508,-153.3948,114.8,3.8,ml,,,,0.48,ak,ak022z3i71m,2022-01-21T23:14:56.388Z,"42 km ESE of Pedro Bay, Alaska",earthquake,,0.2,,,reviewed,ak,ak
2022-01-21T22:00:01.320Z,26.6013,-111.0969,10,4.4,mb,,180,1.247,0.98,us,us7000ge1a,2022-01-22T01:22:39.683Z,"69 km NNE of Loreto, Mexico",earthquake,7.8,2,0.06,80,reviewed,us,us
2022-01-21T21:48:13.946Z,32.6909,131.9728,64.75,4.4,mb,,121,1.747,0.73,us,us7000ge17,2022-01-21T22:08:44.040Z,"29 km SSE of Saiki, Japan",earthquake,5.1,11.9,0.311,3,reviewed,us,us
2022-01-21T21:47:17.950Z,37.4873333,-118.8268333,5.36,0.44,md,8,329,0.1025,0.02,nc,nc73681651,2022-01-21T22:21:26.636Z,"15km WSW of Toms Place, CA",earthquake,0.96,2.63,0.129,8,reviewed,nc,nc
2022-01-21T21:44:32.460Z,33.6875,-116.7328333,15.42,1.32,ml,42,62,0.02827,0.15,ci,ci39919943,2022-01-21T22:00:41.620Z,"6km SSW of Idyllwild, CA",earthquake,0.2,0.36,0.218,26,reviewed,ci,ci
2022-01-21T21:40:48.874Z,62.7879,-149.4325,69.7,1.9,ml,,,,0.58,ak,ak022z312hm,2022-01-21T21:45:33.236Z,"51 km NE of Chase, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-21T21:39:38.410Z,38.8461685,-122.8164978,0.94,0.37,md,8,85,0.01003,0.01,nc,nc73681646,2022-01-21T21:41:17.161Z,"8km WNW of Cobb, CA",earthquake,0.32,1.13,,1,automatic,nc,nc
2022-01-21T21:34:05.620Z,33.4228333,-116.6146667,8.35,1.17,ml,32,97,0.07243,0.15,ci,ci39919935,2022-01-21T21:58:58.679Z,"16km SSE of Anza, CA",earthquake,0.23,0.6,0.125,14,reviewed,ci,ci
2022-01-21T21:32:28.830Z,36.5778351,-121.1566696,7.35,1.38,md,5,164,0.02393,0.03,nc,nc73681641,2022-01-21T21:48:11.630Z,"5km NNW of Pinnacles, CA",earthquake,0.78,1.12,0.15,5,automatic,nc,nc
2022-01-21T21:26:35.464Z,26.7093,-110.9299,10,5.3,mww,,150,1.318,0.92,us,us7000ge0y,2022-01-22T06:38:55.040Z,"85 km SSW of Bahía de Lobos, Mexico",earthquake,7.9,1.9,0.059,28,reviewed,us,us
2022-01-21T21:18:06.160Z,38.7621651,-122.7438354,-0.28,1.72,md,11,116,0.009443,0.06,nc,nc73681621,2022-01-21T22:22:11.818Z,"2km SSE of The Geysers, CA",earthquake,0.52,1.26,,1,automatic,nc,nc
2022-01-21T21:17:43.290Z,38.7541656,-122.7343369,-0.85,2.62,md,45,87,0.01048,0.24,nc,nc73681616,2022-01-21T22:36:11.300Z,"3km SE of The Geysers, CA",earthquake,0.39,1.45,0.16,26,automatic,nc,nc
2022-01-21T21:17:28.300Z,38.7611656,-122.7388306,1.39,1.34,md,15,112,0.009535,0.03,nc,nc73681626,2022-01-21T23:03:10.099Z,"2km SE of The Geysers, CA",earthquake,0.29,0.32,0.1,3,automatic,nc,nc
2022-01-21T21:17:03.650Z,33.4248333,-116.6165,8.14,1.26,ml,40,38,0.0707,0.17,ci,ci39919895,2022-01-21T21:54:32.800Z,"15km SSE of Anza, CA",earthquake,0.21,0.59,0.223,27,reviewed,ci,ci
2022-01-21T21:15:00.980Z,38.7615013,-122.7369995,1.03,0.88,md,8,125,0.00949,0.03,nc,nc73681611,2022-01-21T21:16:36.874Z,"2km SE of The Geysers, CA",earthquake,0.42,0.7,,1,automatic,nc,nc
2022-01-21T21:12:51.914Z,65.7183,-151.679,3,2.5,ml,,,,0.7,ak,ak022z2v2o0,2022-01-21T21:32:22.040Z,"63 km NNE of Tanana, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-21T20:58:57.470Z,38.8479996,-122.8190002,1.94,0.86,md,12,97,0.007467,0.02,nc,nc73681606,2022-01-21T21:00:35.929Z,"9km WNW of Cobb, CA",earthquake,0.34,0.85,,1,automatic,nc,nc
2022-01-21T20:57:48.570Z,39.4311667,-110.3393333,-1.56,1.26,md,4,151,0.01309,0.1,uu,uu60029879,2022-01-21T21:15:20.750Z,"13 km SSE of Sunnyside, Utah",earthquake,1.44,1.17,0.125,4,reviewed,uu,uu
2022-01-21T20:54:10.550Z,60.5876,-151.4267,61.9,1.5,ml,,,,0.53,ak,ak022z2if1x,2022-01-21T21:26:10.875Z,"6 km WSW of Salamatof, Alaska",earthquake,,0.4,,,reviewed,ak,ak
2022-01-21T20:45:33.500Z,33.8651667,-117.4941667,-0.53,0.91,ml,19,63,0.06278,0.25,ci,ci39919847,2022-01-21T21:47:22.282Z,"3km ESE of Home Gardens, CA",quarry blast,0.62,31.61,0.083,10,reviewed,ci,ci
2022-01-21T20:43:45.869Z,7.6146,126.5685,110.66,5.4,mww,,40,1.12,0.81,us,us7000ge0c,2022-01-22T20:47:35.322Z,"4 km NNE of Baganga, Philippines",earthquake,7.3,3.8,0.063,24,reviewed,us,us
2022-01-21T20:34:41.710Z,34.1261667,-80.7311667,4.84,1.94,md,11,65,0.0324,0.25,se,se60143643,2022-01-23T01:37:36.528Z,"7 km SE of Elgin, South Carolina",earthquake,0.77,0.68,0.062,7,reviewed,se,se
2022-01-21T20:31:51.678Z,32.699,132.0166,50.56,4.9,mb,,55,1.78,0.77,us,us7000ge07,2022-01-22T00:15:34.694Z,"29 km SSE of Saiki, Japan",earthquake,5.1,6.5,0.05,136,reviewed,us,us
2022-01-21T20:20:24.274Z,-20.983,-68.8672,110.42,4.3,mb,,47,0.582,1.05,us,us7000ge01,2022-01-21T22:06:22.040Z,"158 km ESE of Iquique, Chile",earthquake,3.8,6.9,0.2,8,reviewed,us,us
2022-01-21T20:19:56.687Z,39.5604,-120.0241,8.5,0.8,ml,9,85.76,0.068,0.0908,nn,nn00832167,2022-01-22T02:37:26.571Z,"4 km NNW of Verdi, California",earthquake,,1.4,0.34,6,reviewed,nn,nn
2022-01-21T20:12:57.320Z,38.8335,-122.8193333,1.5,0.59,md,12,59,0.01241,0.02,nc,nc73681601,2022-01-21T23:00:30.566Z,"8km NW of The Geysers, CA",earthquake,0.28,0.52,,1,reviewed,nc,nc
2022-01-21T20:05:20.282Z,63.2413,-152.0762,0,2.1,ml,,,,0.9,ak,ak022z282mf,2022-01-21T20:17:13.395Z,"37 km SSW of Denali National Park, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-21T20:02:32.070Z,46.0131667,-112.4596667,-2,1.47,ml,18,113,0.066,0.1,mb,mb80536564,2022-01-22T15:46:19.670Z,"5 km E of Butte, Montana",quarry blast,0.38,31.61,0.266,6,reviewed,mb,mb
2022-01-21T20:00:26.150Z,52.0198333333333,178.344,10.74,3.03,ml,4,350,,0.1,av,av91047508,2022-01-22T02:37:52.510Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,3.01,2,0.106984832658976,4,reviewed,av,av
2022-01-21T20:00:25.672Z,52.0681,178.2842,6.12,3.5,ml,,161,0.173,0.1,us,us7000ge2r,2022-01-22T15:53:27.040Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,5,12.7,0.148,8,reviewed,us,us
2022-01-21T20:00:03.150Z,52.0063333333333,178.283666666667,6.29,3.26,ml,4,352,,0.12,av,av91469286,2022-01-22T01:22:53.380Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,3.26,4.63,0.198531425319153,4,reviewed,av,av
2022-01-21T20:00:02.566Z,52.0313,178.3322,16.04,3.4,ml,,160,0.128,0.23,us,us7000ge2u,2022-01-22T15:47:57.040Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,10.7,10.4,0.101,16,reviewed,us,us
2022-01-21T19:59:14.190Z,19.2366666666667,-155.392666666667,31.25,1.69,md,36,142,,0.11,hv,hv72884882,2022-01-21T20:32:18.061Z,"9 km ENE of Pāhala, Hawaii",earthquake,0.53,0.7,0.185444146007912,19,reviewed,hv,hv
2022-01-21T19:55:26.890Z,38.8323326,-122.8186646,1.98,0.36,md,9,81,0.01117,0.02,nc,nc73681596,2022-01-21T19:57:01.154Z,"8km NW of The Geysers, CA",earthquake,0.47,1.3,,1,automatic,nc,nc
2022-01-21T19:50:43.577Z,-20.6839,-175.3949,10,4.8,mb,,148,6.846,0.81,us,us7000ge1p,2022-01-21T22:46:02.040Z,"54 km NNW of Nuku‘alofa, Tonga",earthquake,5.9,1.9,0.121,21,reviewed,us,us
2022-01-21T19:48:23.210Z,43.3948333333333,-123.147666666667,-0.55,1.42,ml,8,118,0.1045,0.09,uw,uw61812141,2022-01-21T20:24:49.250Z,"5 km ESE of Fair Oaks, Oregon",earthquake,0.33,0.47,0.0239091329394003,2,reviewed,uw,uw
2022-01-21T19:38:41.484Z,52.191,178.4116,3.45,4.2,mb,,118,0.231,0.94,us,us7000ge42,2022-01-22T15:14:00.040Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,5.2,6.7,0.085,42,reviewed,us,us
2022-01-21T19:37:48.349Z,61.4232,-150.3101,42,1.9,ml,,,,0.63,ak,ak022z1tk36,2022-01-21T19:42:11.138Z,"17 km SE of Susitna, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-21T19:33:33.690Z,39.4266667,-110.3195,-1.33,1.55,md,7,192,0.005038,0.04,uu,uu60478437,2022-01-21T20:07:36.710Z,"15 km SSE of Sunnyside, Utah",earthquake,0.99,0.18,0.127,7,reviewed,uu,uu
2022-01-21T19:28:22.350Z,36.0245,-117.8283333,1.7,1.01,ml,12,95,0.0448,0.09,ci,ci39919791,2022-01-21T19:57:29.289Z,"11km ESE of Coso Junction, CA",earthquake,0.17,0.2,0.155,3,reviewed,ci,ci
2022-01-21T19:27:22.880Z,39.2703333,-111.9338333,1.28,1.53,md,8,106,0.1835,0.17,uu,uu60478432,2022-01-21T20:02:26.070Z,"8 km NW of Fayette, Utah",earthquake,0.64,10.46,0.4,5,reviewed,uu,uu
2022-01-21T19:24:43.160Z,37.5966682,-122.2034988,11.49,1.93,md,5,161,0.1732,0.02,nc,nc73681591,2022-01-21T22:46:48.026Z,"7km NE of Foster City, CA",earthquake,1,0.6,0.48,2,automatic,nc,nc
2022-01-21T19:21:58.880Z,37.9248352,-122.1269989,4.44,1.42,md,13,155,0.02105,0.09,nc,nc73681586,2022-01-21T21:03:11.715Z,"4km N of Lafayette, CA",earthquake,0.44,0.52,0.14,11,automatic,nc,nc
2022-01-21T19:21:42.830Z,19.1693325042725,-155.488006591797,36.1399993896484,2.1099999,md,34,151,,0.100000001,hv,hv72884852,2022-01-21T19:24:53.250Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.98,0.769999981,1.04999995,3,automatic,hv,hv
2022-01-21T19:20:09.890Z,38.8391685,-122.8153305,0.49,1.18,md,13,69,0.01575,0.02,nc,nc73681581,2022-01-21T20:38:11.570Z,"8km WNW of Cobb, CA",earthquake,0.22,0.77,,1,automatic,nc,nc
2022-01-21T19:18:28.590Z,19.1736660003662,-155.463668823242,32.2799987792969,1.84000003,md,36,154,,0.119999997,hv,hv72884847,2022-01-21T19:21:34.240Z,"Island of Hawaii, Hawaii",earthquake,0.59,0.810000002,0.779999971,7,automatic,hv,hv
2022-01-21T19:17:07.736Z,38.1607,-118.2424,7.1,2,ml,18,86.99,0.206,0.0819,nn,nn00832133,2022-01-21T20:27:49.145Z,"28 km SSW of Mina, Nevada",earthquake,,3.1,0.24,9,reviewed,nn,nn
2022-01-21T19:02:03.810Z,36.7698326,-121.430336,8.88,1.85,md,21,155,0.01474,0.13,nc,nc73681571,2022-01-21T19:59:12.340Z,"8km SW of Ridgemark, CA",earthquake,0.46,0.57,0.28,17,automatic,nc,nc
2022-01-21T18:43:21.993Z,32.668,131.9831,51.28,4.1,mb,,111,1.738,0.84,us,us7000gdyz,2022-01-21T19:11:00.040Z,"31 km ENE of Nobeoka, Japan",earthquake,6.2,2.7,0.214,7,reviewed,us,us
2022-01-21T18:36:44.160Z,33.8606667,-116.8135,15.79,0.2,ml,12,149,0.1689,0.07,ci,ci39919775,2022-01-21T19:54:57.494Z,"7km SSW of Cabazon, CA",earthquake,0.22,0.49,0.02,3,reviewed,ci,ci
2022-01-21T18:35:12.647Z,61.3483,-150.4819,40.2,1.9,ml,,,,0.78,ak,ak022z17mao,2022-01-21T18:38:24.823Z,"Southern Alaska",earthquake,,1.4,,,automatic,ak,ak
2022-01-21T18:33:08.160Z,38.8263333,-122.765,2.73,0.59,md,12,91,0.005639,0.04,nc,nc73681561,2022-01-21T21:08:17.608Z,"4km W of Cobb, CA",earthquake,0.33,0.41,,1,reviewed,nc,nc
2022-01-21T18:29:01.050Z,38.791832,-122.734169,2.01,0.87,md,9,106,0.008812,0.01,nc,nc73681556,2022-01-21T18:30:36.424Z,"2km NE of The Geysers, CA",earthquake,0.38,0.66,0.12,3,automatic,nc,nc
2022-01-21T18:25:45.300Z,39.4161667,-110.3016667,-2.23,1.71,ml,14,199,0.01981,0.15,uu,uu60478422,2022-01-21T19:05:58.810Z,"16 km SSE of Sunnyside, Utah",earthquake,0.46,0.5,0.061,2,reviewed,uu,uu
2022-01-21T18:24:06.930Z,38.8268318,-122.8539963,1.5,0.86,md,12,81,0.002357,0.02,nc,nc73681551,2022-01-21T18:25:41.215Z,"10km WNW of The Geysers, CA",earthquake,0.26,0.44,0.01,2,automatic,nc,nc
2022-01-21T18:17:11.156Z,32.7153,132.0779,45.35,4.6,mb,,100,1.816,1.11,us,us7000gdyu,2022-01-22T11:01:41.812Z,"30 km SSE of Saiki, Japan",earthquake,6.3,8.5,0.116,25,reviewed,us,us
2022-01-21T18:10:52.060Z,51.8636666666667,-177.8585,6.1,0.57,ml,4,216,,0.09,av,av91047488,2022-01-22T01:19:02.300Z,"84 km W of Adak, Alaska",earthquake,0.59,1.18,0.295034333871308,4,reviewed,av,av
2022-01-21T18:02:17.680Z,46.3011667,-111.6248333,-2,1.29,ml,8,160,0.326,0.12,mb,mb80536559,2022-01-22T15:51:27.660Z,"8 km WSW of Townsend, Montana",quarry blast,1.4,31.61,0.206,4,reviewed,mb,mb
2022-01-21T17:57:07.530Z,34.6161667,-117.3343333,-1.14,1.16,ml,16,71,0.05552,0.21,ci,ci39919743,2022-01-21T18:33:56.360Z,"8km ENE of Adelanto, CA",quarry blast,0.66,31.61,0.126,7,reviewed,ci,ci
2022-01-21T17:55:01.072Z,-29.7775,-179.1947,325.12,4.7,mb,,64,1.223,0.66,us,us7000gdyw,2022-01-21T18:47:10.040Z,"Kermadec Islands region",earthquake,10.2,5.3,0.059,96,reviewed,us,us
2022-01-21T17:43:32.052Z,32.6369,132.0406,45.89,4.3,mb,,94,1.755,1.11,us,us7000gdyi,2022-01-21T18:33:00.040Z,"35 km E of Nobeoka, Japan",earthquake,3.7,7.8,0.119,22,reviewed,us,us
2022-01-21T17:31:28.080Z,52.0268333333333,178.351,8.86,2.03,ml,4,349,,0.12,av,av91047483,2022-01-22T00:34:00.940Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,2.61,2.04,0.0849112721612495,4,reviewed,av,av
2022-01-21T17:27:47.980Z,33.6471667,-116.711,14.31,0.59,ml,18,91,0.06389,0.14,ci,ci39919719,2022-01-21T18:04:46.769Z,"10km S of Idyllwild, CA",earthquake,0.38,0.63,0.239,14,reviewed,ci,ci
2022-01-21T17:26:43.179Z,36.22066667,-95.837,0,1.35,ml,72,118,0.3122387281,0.59,ok,ok2022blwp,2022-01-21T17:36:01.495Z,"5 km SSE of Owasso, Oklahoma",quarry blast,,0.6,0.22,27,reviewed,ok,ok
2022-01-21T17:20:36.990Z,19.2373332977295,-155.396499633789,31.4599990844727,1.72000003,md,25,144,,0.129999995,hv,hv72884767,2022-01-21T17:23:42.190Z,"9 km ENE of Pāhala, Hawaii",earthquake,0.72,0.959999979,1.76999998,4,automatic,hv,hv
2022-01-21T16:53:58.810Z,38.8163338,-122.8203354,2.86,0.35,md,8,110,0.01016,0.02,nc,nc73681536,2022-01-21T16:55:34.856Z,"7km NW of The Geysers, CA",earthquake,0.67,1.12,,1,automatic,nc,nc
2022-01-21T16:47:56.288Z,61.2682,-151.5702,71.3,2.3,ml,,,,0.42,ak,ak022z03f1s,2022-01-21T16:52:09.806Z,"29 km WNW of Beluga, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-21T16:44:35.120Z,19.2291660308838,-155.412994384766,33.1399993896484,2.31,ml,44,145,,0.119999997,hv,hv72884757,2022-01-21T16:50:06.310Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.55,0.810000002,0.29,3,automatic,hv,hv
2022-01-21T16:36:50.090Z,61.3723333333333,-151.350833333333,11,1.12,ml,5,207,,0.11,av,av91469221,2022-01-22T00:27:58.030Z,"29 km NNW of Beluga, Alaska",earthquake,0.59,1.22,0.113326802665503,5,reviewed,av,av
2022-01-21T16:33:43.480Z,35.7748333,-117.6065,10.78,1.26,ml,16,131,0.04147,0.13,ci,ci39919647,2022-01-21T18:06:07.114Z,"18km NNE of Ridgecrest, CA",earthquake,0.35,0.45,0.102,14,reviewed,ci,ci
2022-01-21T16:27:46.590Z,19.4895000457764,-155.647659301758,0.639999985694885,1.70000005,md,23,99,,0.25999999,hv,hv72884737,2022-01-21T16:33:17.180Z,"23 km E of Honaunau-Napoopoo, Hawaii",earthquake,0.52,1.57000005,0.870000005,10,automatic,hv,hv
2022-01-21T16:23:18.640Z,38.8390007,-122.8201675,1.38,1.63,md,7,139,0.01197,0.03,nc,nc73681531,2022-01-21T17:36:11.290Z,"9km WNW of Cobb, CA",earthquake,0.48,1.86,0.51,2,automatic,nc,nc
2022-01-21T16:20:23.000Z,38.8429985,-122.8401642,1.32,0.62,md,11,120,0.005721,0.01,nc,nc73681521,2022-01-21T16:21:58.339Z,"10km NW of The Geysers, CA",earthquake,0.29,0.53,0.25,2,automatic,nc,nc
2022-01-21T16:11:52.668Z,-33.9061,179.1303,202.57,4.5,mb,,99,3.709,1,us,us7000gdx1,2022-01-22T21:25:54.040Z,"south of the Kermadec Islands",earthquake,13,12.3,0.145,14,reviewed,us,us
2022-01-21T16:08:37.265Z,32.7437,132.0432,39,6.3,mww,,24,1.825,1.12,us,us7000gdwz,2022-01-23T06:01:21.980Z,"26 km SSE of Saiki, Japan",earthquake,3.9,1.9,0.073,18,reviewed,us,us
2022-01-21T16:07:28.302Z,43.2104,47.8778,10,4.2,mb,,79,2.627,1.12,us,us7000gdx0,2022-01-22T10:44:34.921Z,"30 km ESE of Sulak, Russia",earthquake,7.1,1.5,0.115,21,reviewed,us,us
2022-01-21T16:05:31.080Z,37.4583333,-118.6866667,12.84,0.86,md,7,344,0.1735,0.04,nc,nc73681516,2022-01-21T16:41:55.798Z,"9km WNW of Round Valley, CA",earthquake,3.85,2.61,0.105,7,reviewed,nc,nc
2022-01-21T15:50:27.169Z,60.2491,-143.3863,7.5,2.9,ml,,,,0.52,ak,ak0229pv5mlw,2022-01-21T17:28:36.040Z,"134 km S of McCarthy, Alaska",earthquake,,0.2,,,reviewed,ak,ak
2022-01-21T15:43:23.246Z,-27.9021,-176.6568,10,5.2,mww,,116,1.752,1.22,us,us7000gdwv,2022-01-21T16:19:41.040Z,"Kermadec Islands region",earthquake,10.9,1.9,0.093,11,reviewed,us,us
2022-01-21T15:41:07.440Z,48.4813333333333,-124.7135,7.25,2.15,ml,11,160,0.1383,0.44,uw,uw61812041,2022-01-21T20:29:46.380Z,"14 km NNW of Neah Bay, Washington",earthquake,0.91,2.86,0.181092719093122,6,reviewed,uw,uw
2022-01-21T15:37:49.940Z,33.3656667,-116.3453333,4.81,0.78,ml,32,71,0.03008,0.17,ci,ci39919623,2022-01-21T19:39:48.260Z,"12km NNE of Borrego Springs, CA",earthquake,0.23,0.42,0.185,12,reviewed,ci,ci
2022-01-21T15:17:24.850Z,62.9288,-150.713,25.2,2.2,ml,,,,0.83,ak,ak022yzbhj5,2022-01-21T15:22:39.260Z,"48 km N of Petersville, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-21T15:13:37.921Z,-17.8874,-178.6185,569.54,4.3,mb,,86,3.174,0.95,us,us7000gdvg,2022-01-21T15:37:16.040Z,"219 km E of Levuka, Fiji",earthquake,8.9,7,0.063,72,reviewed,us,us
2022-01-21T15:02:50.575Z,63.0411,-150.8864,0,1.8,ml,,,,0.49,ak,ak022yz8bss,2022-01-21T15:11:17.731Z,"61 km N of Petersville, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-21T14:56:39.540Z,35.084,-118.2315,3.41,0.95,ml,15,67,0.1298,0.12,ci,ci39919567,2022-01-21T19:26:55.864Z,"6km NW of Mojave, CA",earthquake,0.18,0.66,0.152,8,reviewed,ci,ci
2022-01-21T14:55:22.650Z,58.6802,-152.4933,4.3,2.4,ml,,,,0.61,ak,ak022yyy6yx,2022-01-21T15:06:36.957Z,"73 km NNE of Aleneva, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-21T14:53:32.450Z,33.8626667,-116.8108333,14.65,1.06,ml,33,43,0.03109,0.2,ci,ci39919559,2022-01-21T18:07:35.780Z,"6km SSW of Cabazon, CA",earthquake,0.3,0.73,0.241,30,reviewed,ci,ci
2022-01-21T14:43:41.660Z,38.7571667,-122.7178333,1.65,0.21,md,22,95,0.007051,0.03,nc,nc73681501,2022-01-21T22:45:58.528Z,"3km SW of Anderson Springs, CA",earthquake,0.34,0.22,0.032,2,reviewed,nc,nc
2022-01-21T14:33:18.870Z,34.0638333,-117.2263333,13.79,0.79,ml,27,97,0.1423,0.15,ci,ci39919527,2022-01-21T19:15:00.958Z,"4km ENE of Loma Linda, CA",earthquake,0.25,0.62,0.046,6,reviewed,ci,ci
2022-01-21T14:28:38.122Z,61.3652,-140.9748,13.4,1.8,ml,,,,0.37,ak,ak022yysfxm,2022-01-21T14:33:32.977Z,"104 km E of McCarthy, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-21T14:26:34.855Z,38.5498,-119.526,6.8,0.7,ml,10,117.07,0.037,0.1206,nn,nn00832166,2022-01-22T02:37:22.139Z,"2 km SW of Coleville, California",earthquake,,1.3,0.12,2,reviewed,nn,nn
2022-01-21T14:17:28.680Z,19.2146663665771,-155.418502807617,34.0400009155273,2.13000011,md,32,145,,0.180000007,hv,hv72884632,2022-01-21T14:20:39.250Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.62,0.980000019,1.75,6,automatic,hv,hv
2022-01-21T14:14:03.960Z,19.1669998168945,-155.471664428711,32.060001373291,2.39,ml,47,81,,0.100000001,hv,hv72884627,2022-01-22T06:04:34.040Z,"4 km S of Pāhala, Hawaii",earthquake,0.49,0.730000019,4.02,24,automatic,hv,hv
2022-01-21T14:11:05.370Z,38.8363342,-122.7975006,0.07,0.85,md,12,68,0.005961,0.09,nc,nc73681491,2022-01-21T14:12:41.631Z,"7km WNW of Cobb, CA",earthquake,0.34,0.69,,1,automatic,nc,nc
2022-01-21T14:08:54.440Z,33.9915,-116.9563333,17.06,1.73,ml,55,40,0.05892,0.18,ci,ci39919511,2022-01-21T16:09:55.530Z,"7km NNE of Beaumont, CA",earthquake,0.21,0.51,0.207,27,reviewed,ci,ci
2022-01-21T13:59:45.040Z,38.7895012,-122.7791672,1.19,0.85,md,12,117,0.007762,0.03,nc,nc73681486,2022-01-21T14:01:21.387Z,"2km NW of The Geysers, CA",earthquake,0.31,0.66,,1,automatic,nc,nc
2022-01-21T13:58:26.840Z,38.7708321,-122.7638321,-0.89,0.78,md,7,157,0.001501,0.31,nc,nc73681481,2022-01-21T14:00:02.062Z,"1km SW of The Geysers, CA",earthquake,2.05,2.67,0.06,2,automatic,nc,nc
2022-01-21T13:55:40.040Z,36.2456667,-120.4003333,7.14,1.1,md,13,153,0.09182,0.04,nc,nc73681476,2022-01-21T21:57:10.678Z,"12km NNW of Coalinga, CA",earthquake,0.82,1.05,0.21,6,reviewed,nc,nc
2022-01-21T13:55:27.796Z,61.7203,-151.2942,65.3,2.5,ml,,,,0.56,ak,ak022yycrra,2022-01-21T14:06:09.868Z,"30 km S of Skwentna, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-21T13:43:50.490Z,36.1656667,-118.0215,2.36,1.26,ml,15,81,0.1432,0.11,ci,ci39919487,2022-01-21T16:09:48.882Z,"13km S of Olancha, CA",earthquake,0.25,1.33,0.225,17,reviewed,ci,ci
2022-01-21T13:32:28.874Z,28.1052,52.1647,10,4.4,mb,,78,4.795,0.48,us,us7000gduy,2022-01-22T10:47:38.483Z,"91 km SSW of Fīrūzābād, Iran",earthquake,8,1.5,0.107,25,reviewed,us,us
2022-01-21T13:31:31.120Z,19.1788330078125,-155.491165161133,31.7399997711182,2.29999995,md,40,140,,0.119999997,hv,hv72884582,2022-01-21T13:35:04.870Z,"2 km SSW of Pāhala, Hawaii",earthquake,0.51,0.899999976,1.30999994,19,automatic,hv,hv
2022-01-21T13:28:28.320Z,37.6283333,-118.8448333,7.96,0.22,md,14,87,0.007216,0.13,nc,nc73681471,2022-01-21T16:31:55.692Z,"12km E of Mammoth Lakes, CA",earthquake,0.71,1.51,0.231,13,reviewed,nc,nc
2022-01-21T13:25:25.820Z,44.8043333,-110.8051667,7.26,0.43,md,7,297,0.03603,0.09,uu,uu60478407,2022-01-21T15:11:02.940Z,"20 km SSW of Mammoth, Wyoming",earthquake,1.66,1.03,0.262,6,reviewed,uu,uu
2022-01-21T13:24:55.460Z,36.70066667,-97.67733333,8.83,2.67,ml,75,54,0,0.14,ok,ok2022blop,2022-01-21T14:09:44.736Z,"10 km ESE of Jefferson, Oklahoma",earthquake,,3.1,0.28,35,reviewed,ok,ok
2022-01-21T13:22:33.351Z,-20.7823,-175.3815,10,4.8,mb,,86,6.898,0.39,us,us7000ge1f,2022-01-21T22:32:05.040Z,"43 km NNW of Nuku‘alofa, Tonga",earthquake,6.3,1.9,0.149,14,reviewed,us,us
2022-01-21T13:19:59.220Z,19.1485004425049,-155.427505493164,31.5100002288818,1.85000002,md,22,179,,0.109999999,hv,hv72884567,2022-01-21T13:23:02.110Z,"8 km SE of Pāhala, Hawaii",earthquake,0.95,0.769999981,0.860000014,7,automatic,hv,hv
2022-01-21T13:12:35.260Z,38.8311653,-122.8014984,1.47,0.85,md,7,118,0.01025,0,nc,nc73681466,2022-01-21T13:14:11.928Z,"7km W of Cobb, CA",earthquake,0.68,1.63,,1,automatic,nc,nc
2022-01-21T13:11:05.190Z,19.1895008087158,-155.473663330078,34.0400009155273,1.75999999,md,41,94,,0.129999995,hv,hv72884562,2022-01-21T13:14:18.920Z,"1 km SSE of Pāhala, Hawaii",earthquake,0.57,0.819999993,0.870000005,8,automatic,hv,hv
2022-01-21T13:05:01.700Z,33.3775,-116.877,5.58,1.55,ml,61,25,0.02668,0.21,ci,ci39919455,2022-01-21T19:49:26.570Z,"3km NNW of Palomar Observatory, CA",earthquake,0.19,0.6,0.116,24,reviewed,ci,ci
2022-01-21T13:03:21.450Z,38.8170013,-122.7638321,1.5,1.17,md,12,166,0.01369,0.03,nc,nc73681456,2022-01-21T13:36:10.797Z,"4km W of Cobb, CA",earthquake,0.42,0.75,,1,automatic,nc,nc
2022-01-21T12:59:34.357Z,31.67671232,-104.3795789,7.519799805,3.3,ml,36,55,0.09789568326,0.2,tx,tx2022blnu,2022-01-21T22:47:54.565Z,"55 km S of Whites City, New Mexico",earthquake,0.9087192477,1.151815376,0.1,19,reviewed,tx,tx
2022-01-21T12:54:32.270Z,17.9141,-66.8455,15,2.93,md,21,192,0.0697,0.15,pr,pr2022021006,2022-01-21T13:17:25.642Z,"8 km SSE of Maria Antonia, Puerto Rico",earthquake,0.64,0.66,0.2,11,reviewed,pr,pr
2022-01-21T12:53:33.781Z,62.0535,-151.35,89.9,2,ml,,,,0.43,ak,ak022yxqx6o,2022-01-21T13:02:22.483Z,"7 km NNE of Skwentna, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-21T12:48:37.120Z,19.2213325500488,-155.427169799805,31.7099990844727,2.28,ml,46,130,,0.129999995,hv,hv72884532,2022-01-22T06:28:30.040Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.43,0.699999988,0.23,8,automatic,hv,hv
2022-01-21T12:43:02.600Z,38.7898331,-122.7798309,3.85,0.57,md,10,100,0.007149,0.02,nc,nc73681451,2022-01-21T12:44:36.037Z,"2km NW of The Geysers, CA",earthquake,0.43,1.17,0.34,2,automatic,nc,nc
2022-01-21T12:34:55.470Z,38.1868,-117.7699,7.9,1.3,ml,15,155.14,0.12,0.1073,nn,nn00832125,2022-01-21T19:16:53.494Z,"37 km SE of Mina, Nevada",earthquake,,2.1,0.15,6,reviewed,nn,nn
2022-01-21T12:01:56.650Z,39.0083333,-111.446,1.94,1.76,md,6,122,0.2287,0.07,uu,uu60478402,2022-01-21T16:57:12.310Z,"19 km WNW of Emery, Utah",earthquake,0.88,31.61,0.238,5,reviewed,uu,uu
2022-01-21T11:59:05.238Z,6.5248,126.9375,104.25,4.7,mb,,74,1.453,0.53,us,us7000gdug,2022-01-22T11:02:14.151Z,"77 km ESE of Bobon, Philippines",earthquake,7.8,6.9,0.077,51,reviewed,us,us
2022-01-21T11:50:26.000Z,34.0355,-117.5568333,9.95,1.07,ml,50,61,0.03108,0.13,ci,ci39919407,2022-01-21T19:41:18.090Z,"6km NW of Mira Loma, CA",earthquake,0.16,0.29,0.133,23,reviewed,ci,ci
2022-01-21T11:45:06.400Z,55.1615,-162.262666666667,4.84,-0.37,ml,4,221,,0.12,av,av91047478,2022-01-22T00:06:22.150Z,"11 km NNE of King Cove, Alaska",earthquake,2.37,0.57,0.0794121987373932,4,reviewed,av,av
2022-01-21T11:37:28.020Z,35.9871667,-91.7881667,1.57,2.1,md,8,141,0.2893,0.19,nm,nm60143543,2022-01-21T14:43:53.310Z,"4 km NW of Mount Pleasant, Arkansas",earthquake,0.59,3.6,0.088,8,reviewed,nm,nm
2022-01-21T11:35:37.570Z,19.1615,-155.475,32.07,2.78,ml,53,108,,0.11,hv,hv72884497,2022-01-21T20:23:23.130Z,"4 km S of Pāhala, Hawaii",earthquake,0.4,0.49,0.166170320338557,34,reviewed,hv,hv
2022-01-21T11:24:46.994Z,38.1509,-117.9618,9.8,0.7,ml,13,131.04,0.012,0.1387,nn,nn00832124,2022-01-21T18:39:32.456Z,"Nevada",earthquake,,1,0.46,5,reviewed,nn,nn
2022-01-21T11:24:38.630Z,33.5915,-116.8085,4.52,0.19,ml,21,66,0.03712,0.1,ci,ci39919399,2022-01-21T19:30:06.700Z,"13km WNW of Anza, CA",earthquake,0.17,0.23,0.143,8,reviewed,ci,ci
2022-01-21T11:07:02.220Z,39.1933333,-111.9131667,5.66,1.38,md,5,171,0.1724,0.06,uu,uu60478397,2022-01-21T16:49:59.010Z,"6 km SW of Fayette, Utah",earthquake,1.17,6.93,0.396,3,reviewed,uu,uu
2022-01-21T11:02:34.160Z,35.6545,-117.541,2.22,0.66,ml,11,140,0.09341,0.13,ci,ci39919391,2022-01-21T13:43:38.907Z,"13km ENE of Ridgecrest, CA",earthquake,0.47,0.88,0.08,7,reviewed,ci,ci
2022-01-21T10:59:39.770Z,35.5953333,-117.4121667,8.73,0.83,ml,8,170,0.04172,0.13,ci,ci39919383,2022-01-21T13:43:39.906Z,"19km S of Trona, CA",earthquake,1.57,0.89,0.376,3,reviewed,ci,ci
2022-01-21T10:57:49.030Z,34.0215,-117.2305,19.14,0.76,ml,23,131,0.08813,0.14,ci,ci39919375,2022-01-21T19:25:06.313Z,"4km SE of Loma Linda, CA",earthquake,0.32,0.43,0.11,10,reviewed,ci,ci
2022-01-21T10:57:08.710Z,33.7043333,-116.729,16.47,0.53,ml,8,143,0.01412,0.07,ci,ci39919367,2022-01-21T13:44:09.703Z,"4km SSW of Idyllwild, CA",earthquake,0.34,0.38,0.104,8,reviewed,ci,ci
2022-01-21T10:57:07.920Z,60.32,-152.7415,13.96,-0.21,ml,7,333,,0.09,av,av91047473,2022-01-22T00:02:29.830Z,"66 km WNW of Ninilchik, Alaska",earthquake,1.07,0.69,0.111647879848572,7,reviewed,av,av
2022-01-21T10:50:39.210Z,38.7593333,-122.9461667,6.34,1.38,md,44,108,0.05462,0.05,nc,nc73681441,2022-01-22T01:15:10.938Z,"8km SE of Cloverdale, CA",earthquake,0.25,0.52,0.147,14,reviewed,nc,nc
2022-01-21T10:39:08.350Z,38.840168,-122.8241653,1.89,0.37,md,8,92,0.008981,0.01,nc,nc73681436,2022-01-21T10:40:46.714Z,"9km WNW of Cobb, CA",earthquake,0.41,1,,1,automatic,nc,nc
2022-01-21T10:29:18.400Z,32.8988333,-115.5148333,8.02,1.4,ml,18,106,0.03868,0.17,ci,ci39919359,2022-01-21T19:20:37.991Z,"8km NE of Imperial, CA",earthquake,0.37,0.34,0.201,12,reviewed,ci,ci
2022-01-21T10:28:17.380Z,33.445,-116.5441667,10.15,1.78,ml,86,22,0.0702,0.18,ci,ci39919351,2022-01-21T19:07:54.230Z,"17km SE of Anza, CA",earthquake,0.12,0.24,0.223,24,reviewed,ci,ci
2022-01-21T10:28:08.390Z,32.8893333,-115.5205,8.28,1.28,ml,14,73,0.03593,0.15,ci,ci39919343,2022-01-21T18:52:11.821Z,"6km NE of Imperial, CA",earthquake,0.36,0.49,0.17,13,reviewed,ci,ci
2022-01-21T10:20:05.070Z,34.6273333,-118.9328333,10.47,0.99,ml,17,52,0.1453,0.28,ci,ci39919335,2022-01-21T17:55:43.471Z,"20km SSW of Gorman, CA",earthquake,0.39,1.08,0.197,4,reviewed,ci,ci
2022-01-21T10:12:31.972Z,23.0823,93.8207,58.69,5.4,mww,,22,3.768,0.8,us,us7000gdtu,2022-01-22T10:17:09.636Z,"23 km NE of Falam, Myanmar",earthquake,7.5,4.5,0.075,17,reviewed,us,us
2022-01-21T10:06:53.630Z,19.2333333333333,-155.380166666667,32.9,1.43,md,17,153,,0.12,hv,hv72884397,2022-01-21T20:41:46.620Z,"10 km ENE of Pāhala, Hawaii",earthquake,0.82,0.84,0.060973280867112,10,reviewed,hv,hv
2022-01-21T10:05:50.650Z,37.5143333,-118.824,9.42,1.14,md,21,118,0.07567,0.04,nc,nc73681426,2022-01-21T17:10:11.130Z,"14km WSW of Toms Place, CA",earthquake,0.28,0.69,0.103,19,reviewed,nc,nc
2022-01-21T10:05:04.370Z,37.5051667,-118.8345,7.32,1.54,md,23,120,0.08482,0.07,nc,nc73681421,2022-01-21T16:43:10.984Z,"15km WSW of Toms Place, CA",earthquake,0.24,0.89,0.098,22,reviewed,nc,nc
2022-01-21T10:04:11.620Z,57.7665,-138.5838,10,3.3,ml,,196,1.272,0.49,us,us7000gdtr,2022-01-21T10:54:36.040Z,"140 km WSW of Elfin Cove, Alaska",earthquake,4,1.9,0.053,47,reviewed,us,us
2022-01-21T09:50:42.680Z,39.7113333,-123.4098333,8.47,1.84,md,24,77,0.07331,0.08,nc,nc73681416,2022-01-22T00:50:10.692Z,"7km ENE of Laytonville, CA",earthquake,0.19,0.43,0.149,21,reviewed,nc,nc
2022-01-21T09:43:06.810Z,38.8390007,-122.8805008,2.55,0.34,md,8,131,0.002433,0.01,nc,nc73681406,2022-01-21T09:44:40.687Z,"12km ENE of Cloverdale, CA",earthquake,0.8,0.73,,1,automatic,nc,nc
2022-01-21T09:30:10.360Z,38.8328323,-122.8191681,1.57,1.21,md,24,57,0.0118,0.02,nc,nc73681401,2022-01-21T10:06:10.336Z,"8km NW of The Geysers, CA",earthquake,0.18,0.44,0.08,4,automatic,nc,nc
2022-01-21T09:28:50.910Z,35.8735,-117.6393333,12.32,0.41,ml,5,155,0.06691,0.04,ci,ci39919319,2022-01-21T13:45:11.987Z,"24km WNW of Searles Valley, CA",earthquake,0.37,0.58,0.047,4,reviewed,ci,ci
2022-01-21T09:24:15.910Z,35.879,-117.6248333,13.84,0.61,ml,6,142,0.05962,0.12,ci,ci39919311,2022-01-21T13:45:14.202Z,"24km WNW of Searles Valley, CA",earthquake,0.53,0.89,0.075,5,reviewed,ci,ci
2022-01-21T09:16:01.070Z,17.9618,-66.7496,11,2.6,md,15,187,0.1303,0.13,pr,pr2022021005,2022-01-21T10:00:47.614Z,"5 km SW of Tallaboa, Puerto Rico",earthquake,0.49,0.42,0.25,6,reviewed,pr,pr
2022-01-21T09:14:51.570Z,35.6671667,-117.483,4.78,0.6,ml,10,163,0.08226,0.16,ci,ci39919303,2022-01-21T13:45:32.272Z,"13km SSW of Searles Valley, CA",earthquake,0.66,0.74,0.168,7,reviewed,ci,ci
2022-01-21T09:10:51.100Z,40.5439987,-122.0554962,11.66,1.98,md,8,106,0.07817,0.12,nc,nc73681391,2022-01-21T09:40:11.177Z,"11km E of Millville, CA",earthquake,0.54,1.46,0.13,7,automatic,nc,nc
2022-01-21T09:01:45.755Z,38.1837,-117.8063,8,1.6,ml,16,110.62,0.129,0.1422,nn,nn00832120,2022-01-21T17:28:26.137Z,"35 km SE of Mina, Nevada",earthquake,,3.1,0.15,7,reviewed,nn,nn
2022-01-21T08:53:28.717Z,38.7349,-119.7195,6,0.7,ml,8,92.89,0.166,0.0875,nn,nn00832163,2022-01-22T02:37:19.168Z,"7 km NE of Markleeville, California",earthquake,,4.2,0.41,4,reviewed,nn,nn
2022-01-21T08:48:25.380Z,38.8424988,-122.8781662,2.61,0.39,md,12,94,0.005939,0.02,nc,nc73681386,2022-01-21T08:50:00.617Z,"13km ENE of Cloverdale, CA",earthquake,0.4,0.66,0.23,3,automatic,nc,nc
2022-01-21T08:47:39.500Z,17.8103,-66.913,11,2.07,md,5,302,0.1682,0.26,pr,pr2022021004,2022-01-21T09:08:04.666Z,"17 km S of Guánica, Puerto Rico",earthquake,1.36,1.91,0,1,reviewed,pr,pr
2022-01-21T08:43:44.680Z,38.8258324,-122.8539963,2.31,0.67,md,11,124,0.002824,0.04,nc,nc73681381,2022-01-21T08:45:21.583Z,"10km WNW of The Geysers, CA",earthquake,0.41,0.58,0.24,2,automatic,nc,nc
2022-01-21T08:37:50.030Z,44.7913333,-110.8868333,8.19,0.41,md,9,111,0.02605,0.15,uu,uu60478387,2022-01-21T15:03:49.610Z,"22 km NE of West Yellowstone, Montana",earthquake,0.55,0.87,0.341,6,reviewed,uu,uu
2022-01-21T08:15:16.901Z,36.9445,-116.1096,5.6,0.1,ml,11,85.12,0.045,0.1332,nn,nn00832152,2022-01-21T22:00:33.440Z,"57 km NW of Indian Springs, Nevada",earthquake,,1.8,0.46,5,reviewed,nn,nn
2022-01-21T08:14:59.020Z,44.457,-115.2136667,7.35,1.91,ml,9,82,0.843,0.19,mb,mb80536544,2022-01-21T15:12:02.460Z,"34 km NW of Stanley, Idaho",earthquake,0.6,1.12,0.141,8,reviewed,mb,mb
2022-01-21T08:02:14.430Z,19.4093341827393,-155.26432800293,1.25,1.9,ml,13,64,,0.119999997,hv,hv72884227,2022-01-21T08:07:44.490Z,"4 km SW of Volcano, Hawaii",earthquake,0.24,0.200000003,0.32,10,automatic,hv,hv
2022-01-21T07:58:53.012Z,62.654,-151.6538,4.5,1.6,ml,,,,0.44,ak,ak022yusv85,2022-01-21T10:26:05.551Z,"48 km WNW of Petersville, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-21T07:54:33.230Z,33.3831667,-116.8751667,5.42,0.34,ml,22,54,0.03128,0.14,ci,ci39919271,2022-01-21T18:49:22.854Z,"3km NNW of Palomar Observatory, CA",earthquake,0.21,0.56,0.149,7,reviewed,ci,ci
2022-01-21T07:52:57.820Z,18.019,-66.7621,14,2.46,md,10,169,0.1251,0.11,pr,pr2022021003,2022-01-21T08:04:30.246Z,"0 km ENE of Magas Arriba, Puerto Rico",earthquake,0.38,0.59,0.31,2,reviewed,pr,pr
2022-01-21T07:47:21.860Z,19.3838333333333,-155.041666666667,4.87,1.52,md,38,163,,0.16,hv,hv72884197,2022-01-21T21:09:02.180Z,"13 km SE of Fern Forest, Hawaii",earthquake,0.35,0.33,0.123232476107218,19,reviewed,hv,hv
2022-01-21T07:34:46.942Z,36.4238,-115.7739,0,0.6,ml,9,303.26,0.349,0.1467,nn,nn00832143,2022-01-21T21:32:39.678Z,"18 km SSW of Indian Springs, Nevada",earthquake,,0,0.94,4,reviewed,nn,nn
2022-01-21T07:20:56.446Z,31.61632489,-104.334395,7.416967772999999,2.3,ml,39,62,0.08110429088,0.3,tx,tx2022blcp,2022-01-21T23:37:54.148Z,"61 km WNW of Toyah, Texas",earthquake,0.8724375574,0.8956844525,0.2,21,reviewed,tx,tx
2022-01-21T07:19:21.300Z,19.1843338012695,-155.464828491211,34.8899993896484,2.24000001,md,44,103,,0.129999995,hv,hv72884167,2022-01-21T07:22:25.650Z,"2 km SE of Pāhala, Hawaii",earthquake,0.62,0.829999983,0.159999996,25,automatic,hv,hv
2022-01-21T07:14:13.830Z,18.0121,-66.7681,14,2.32,md,10,173,0.1171,0.08,pr,pr2022021002,2022-01-21T07:33:25.824Z,"Puerto Rico region",earthquake,0.55,0.49,0.12,5,reviewed,pr,pr
2022-01-21T07:13:15.843Z,38.125,-118.3862,13.6,0.4,ml,6,309.54,0.157,0.0327,nn,nn00832162,2022-01-21T23:33:19.222Z,"34 km NNE of Benton, California",earthquake,,25.7,0,1,reviewed,nn,nn
2022-01-21T07:00:40.420Z,38.8338318,-122.8174973,1.68,1.18,md,19,58,0.01193,0.02,nc,nc73681376,2022-01-21T08:14:11.105Z,"8km NW of The Geysers, CA",earthquake,0.21,0.58,0.01,3,automatic,nc,nc
2022-01-21T06:58:42.872Z,12.9047,144.1948,7.14,5.2,mww,,57,0.945,0.67,us,us7000gdsi,2022-01-22T07:08:49.409Z,"65 km SW of Merizo Village, Guam",earthquake,7.9,4.5,0.089,12,reviewed,us,us
2022-01-21T06:54:46.410Z,-20.7746,-69.2387,103.59,3.6,mb,,94,0.354,0.47,us,us7000gdsb,2022-01-21T09:19:38.441Z,"113 km ESE of Iquique, Chile",earthquake,5.7,9.8,0.352,2,reviewed,us,us
2022-01-21T06:50:17.618Z,38.1518,-117.9385,12.3,1,ml,14,128.67,0.021,0.1106,nn,nn00832119,2022-01-21T18:27:06.976Z,"30 km SSE of Mina, Nevada",earthquake,,1,0.36,4,reviewed,nn,nn
2022-01-21T06:43:25.800Z,51.87,-176.612333333333,3.63,1.58,ml,4,269,,0.1,av,av91047468,2022-01-21T23:55:52.840Z,"1 km ESE of Adak, Alaska",earthquake,1,0.63,0.109040303978829,4,reviewed,av,av
2022-01-21T06:36:00.670Z,59.974,-153.0715,1.26,0.08,ml,4,145,,0.09,av,av91468936,2022-01-21T23:53:46.340Z,"61 km ENE of Pedro Bay, Alaska",earthquake,0.34,0.35,0.207223906288478,4,reviewed,av,av
2022-01-21T06:28:10.090Z,17.9281,-66.6953,17,2.84,md,15,174,0.1452,0.12,pr,pr2022021001,2022-01-21T06:48:11.731Z,"7 km SSE of Tallaboa, Puerto Rico",earthquake,0.34,0.28,0.08,6,reviewed,pr,pr
2022-01-21T06:12:59.859Z,16.6075,-99.5721,10,4.3,mb,,257,1.351,0.57,us,us7000gds4,2022-01-21T16:00:35.136Z,"11 km SE of San Andrés Playa Encantada (El Podrido), Mexico",earthquake,10.6,2,0.147,13,reviewed,us,us
2022-01-21T06:08:29.920Z,33.7015,-116.8133333,14.9,0.36,ml,17,92,0.07689,0.16,ci,ci37380924,2022-01-21T17:39:11.966Z,"9km SE of Valle Vista, CA",earthquake,0.43,0.73,0.167,8,reviewed,ci,ci
2022-01-21T06:08:24.520Z,33.7151667,-116.8108333,14.64,0.44,ml,24,176,0.08067,0.13,ci,ci39919247,2022-01-21T17:33:21.688Z,"8km ESE of Valle Vista, CA",earthquake,0.33,0.28,0.163,9,reviewed,ci,ci
2022-01-21T06:00:37.440Z,38.831665,-122.81633,1.52,1.08,md,20,52,0.009595,0.02,nc,nc73681361,2022-01-21T06:02:14.285Z,"8km NW of The Geysers, CA",earthquake,0.21,0.4,0.14,2,automatic,nc,nc
2022-01-21T05:55:51.880Z,19.2038326263428,-155.425506591797,31.8899993896484,2.34,ml,30,149,,0.109999999,hv,hv72884047,2022-01-21T06:01:23.740Z,"5 km E of Pāhala, Hawaii",earthquake,0.55,0.870000005,0.44,12,automatic,hv,hv
2022-01-21T05:49:55.070Z,33.6043333,-116.6375,14.64,2.12,ml,11,145,0.03517,0.05,ci,ci39919231,2022-01-21T17:25:38.289Z,"6km NNE of Anza, CA",earthquake,0.3,0.45,0.346,6,reviewed,ci,ci
2022-01-21T05:46:15.790Z,19.2210006713867,-155.432662963867,32.3400001525879,2.26,ml,43,131,,0.119999997,hv,hv72884037,2022-01-21T05:51:46.140Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.51,0.800000012,4.54,4,automatic,hv,hv
2022-01-21T05:45:58.910Z,19.3318333333333,-155.123833333333,4.6,1.43,md,25,136,,0.13,hv,hv72884032,2022-01-21T21:20:55.440Z,"14 km S of Fern Forest, Hawaii",earthquake,0.37,0.93,0.151066177073341,10,reviewed,hv,hv
2022-01-21T05:45:58.017Z,-20.7481,-175.3195,10,4.7,mb,,123,6.936,0.57,us,us7000gdrz,2022-01-21T06:15:00.040Z,"45 km NNW of Nuku‘alofa, Tonga",earthquake,13.8,1.7,0.147,14,reviewed,us,us
2022-01-21T05:43:35.670Z,36.0886667,-117.8606667,3.56,1.34,ml,18,69,0.02923,0.1,ci,ci39919215,2022-01-21T13:46:20.968Z,"9km ENE of Coso Junction, CA",earthquake,0.19,0.33,0.283,17,reviewed,ci,ci
2022-01-21T05:40:18.630Z,33.7398333,-116.8913333,3.99,-0.35,ml,6,207,0.05918,0.07,ci,ci39919223,2022-01-21T17:19:44.248Z,"1km SSE of Valle Vista, CA",earthquake,0.35,0.93,0.185,3,reviewed,ci,ci
2022-01-21T05:31:42.750Z,38.8079987,-122.822998,2.47,0.57,md,11,65,0.004906,0.02,nc,nc73681356,2022-01-21T05:33:20.032Z,"7km WNW of The Geysers, CA",earthquake,0.3,0.88,0.34,2,automatic,nc,nc
2022-01-21T05:25:43.440Z,44.5355,-115.2211667,3.54,2.06,ml,10,98,0.782,0.17,mb,mb80536539,2022-01-21T15:20:52.270Z,"41 km NNW of Stanley, Idaho",earthquake,0.55,1.91,0.138,11,reviewed,mb,mb
2022-01-21T05:18:26.323Z,60.3208,-152.372,117.3,5.1,mww,,,,0.57,ak,ak022ytdd55,2022-01-23T05:29:00.928Z,"49 km NW of Ninilchik, Alaska",earthquake,,0.3,,,reviewed,ak,ak
2022-01-21T05:15:55.310Z,35.3193333,-118.5238333,5.36,1.65,ml,36,72,0.0888,0.12,ci,ci39919199,2022-01-21T18:46:43.280Z,"22km NNW of Tehachapi, CA",earthquake,0.14,0.6,0.259,26,reviewed,ci,ci
2022-01-21T05:11:16.480Z,38.7994995,-122.793663,3.08,0.35,md,9,72,0.007745,0.01,nc,nc73681346,2022-01-21T05:12:54.254Z,"4km NW of The Geysers, CA",earthquake,0.56,1.75,,1,automatic,nc,nc
2022-01-21T04:59:44.719Z,40.8514,-116.1946,10.2,3,ml,11,102.26,0.132,0.154,nn,nn00832115,2022-01-21T05:24:11.379Z,"17 km NNW of Carlin, Nevada",earthquake,,1.5,0.27,8,reviewed,nn,nn
2022-01-21T04:58:34.659Z,38.1572,-117.9379,12.4,1.1,ml,14,145.67,0.025,0.1082,nn,nn00832114,2022-01-21T17:46:58.947Z,"29 km SSE of Mina, Nevada",earthquake,,0.9,1.1,6,reviewed,nn,nn
2022-01-21T04:57:14.600Z,33.3638333,-116.3375,4.64,0.58,ml,27,110,0.02339,0.18,ci,ci39919191,2022-01-21T19:05:05.889Z,"12km NNE of Borrego Springs, CA",earthquake,0.38,0.43,0.218,11,reviewed,ci,ci
2022-01-21T04:56:59.970Z,38.8344994,-122.8101654,2.28,1.15,md,25,46,0.01109,0.02,nc,nc73681336,2022-01-21T05:21:12.647Z,"8km W of Cobb, CA",earthquake,0.2,0.44,0.12,4,automatic,nc,nc
2022-01-21T04:55:54.580Z,40.2981667,-124.5875,19.83,2.64,md,35,236,0.1876,0.15,nc,nc73681331,2022-01-22T01:31:11.036Z,"26km W of Petrolia, CA",earthquake,1.09,0.26,0.109,34,reviewed,nc,nc
2022-01-21T04:53:17.600Z,33.9188333,-116.0406667,2.35,0.68,ml,14,193,0.08887,0.15,ci,ci39919183,2022-01-21T17:00:42.746Z,"25km S of Twentynine Palms, CA",earthquake,0.47,0.34,0.131,10,reviewed,ci,ci
2022-01-21T04:52:59.340Z,36.0313333,-117.8155,-0.27,0.32,ml,12,91,0.04118,0.12,ci,ci37380764,2022-01-21T16:56:08.253Z,"12km E of Coso Junction, CA",earthquake,0.18,0.6,0.166,4,reviewed,ci,ci
2022-01-21T04:47:27.770Z,34.9676667,-84.7133333,14.82,2.94,md,29,44,0.1103,0.13,se,se60379886,2022-01-23T02:18:38.263Z,"16 km NNE of Eton, Georgia",earthquake,0.25,0.62,0.175,23,reviewed,se,se
2022-01-21T04:47:06.020Z,39.4205,-110.3096667,-1.62,1.63,md,7,196,0.01248,0.12,uu,uu60478372,2022-01-21T16:40:12.560Z,"16 km SSE of Sunnyside, Utah",earthquake,1.19,0.79,0.236,7,reviewed,uu,uu
2022-01-21T04:42:15.670Z,35.9083333,-117.7351667,3.38,1.97,ml,28,43,0.07851,0.15,ci,ci39919175,2022-01-21T13:47:06.690Z,"16km ESE of Little Lake, CA",earthquake,0.21,0.72,0.238,25,reviewed,ci,ci
2022-01-21T04:34:30.293Z,62.6135,-151.4716,12.9,1.4,ml,,,,0.54,ak,ak022ysvdh0,2022-01-21T04:39:19.362Z,"38 km WNW of Petersville, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-21T04:33:55.340Z,35.10933333,-95.53283333,7.74,1.96,ml,53,87,0.106179164,0.2,ok,ok2022bkxc,2022-01-21T14:47:07.576Z,"12 km E of Crowder, Oklahoma",earthquake,,0.5,0.37,6,reviewed,ok,ok
2022-01-21T04:25:38.040Z,34.1551667,-118.0473333,10.42,0.63,ml,10,194,0.06889,0.12,ci,ci39919159,2022-01-21T17:12:52.208Z,"1km SE of Sierra Madre, CA",earthquake,0.39,0.69,0.09,5,reviewed,ci,ci
2022-01-21T04:25:13.519Z,39.4185,-120.5552,7.7,0.7,ml,7,215.29,0.188,0.1427,nn,nn00832161,2022-01-21T23:30:12.550Z,"15 km NW of Kingvale, California",earthquake,,3.7,0.24,3,reviewed,nn,nn
2022-01-21T04:19:51.570Z,38.8196678,-122.7963333,3.21,0.96,md,28,31,0.01136,0.02,nc,nc73681316,2022-01-21T04:21:28.430Z,"6km NW of The Geysers, CA",earthquake,0.22,0.47,0.07,4,automatic,nc,nc
2022-01-21T04:11:36.900Z,35.5165,-118.379,8.48,1.17,ml,16,97,0.1652,0.15,ci,ci39919143,2022-01-21T13:48:09.680Z,"13km SE of Bodfish, CA",earthquake,0.3,1.19,0.181,14,reviewed,ci,ci
2022-01-21T04:05:55.020Z,19.2059993743896,-155.399002075195,31.0900001525879,2.14,ml,45,157,,0.129999995,hv,hv72883917,2022-01-21T04:11:27.540Z,"8 km E of Pāhala, Hawaii",earthquake,0.61,0.730000019,4.3,6,automatic,hv,hv
2022-01-21T03:53:02.150Z,38.7999992,-122.7516632,2.23,0.7,md,15,100,0.00632,0.02,nc,nc73681311,2022-01-21T03:54:40.208Z,"3km N of The Geysers, CA",earthquake,0.33,0.68,0.16,2,automatic,nc,nc
2022-01-21T03:44:58.034Z,38.784,-118.7594,7.9,1,ml,8,138.96,0.425,0.061,nn,nn00832159,2022-01-21T23:20:53.534Z,"15 km N of Walker Lake, Nevada",earthquake,,31.4,0.02,2,reviewed,nn,nn
2022-01-21T03:28:41.080Z,58.3046,-151.9196,42.3,2.9,ml,,,,0.66,ak,ak022ys8ocw,2022-01-21T05:32:55.805Z,"54 km NE of Ouzinkie, Alaska",earthquake,,1.7,,,automatic,ak,ak
2022-01-21T03:25:06.840Z,39.4173333,-110.3051667,-3.03,1.85,md,9,198,0.01685,0.16,uu,uu60478367,2022-01-21T16:39:07.590Z,"16 km SSE of Sunnyside, Utah",earthquake,0.9,2.83,0.133,9,reviewed,uu,uu
2022-01-21T03:24:10.910Z,19.2175006866455,-155.424163818359,32.1500015258789,2.14,ml,27,135,,0.170000002,hv,hv72883867,2022-01-21T03:29:42.840Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.68,0.879999995,0.51,3,automatic,hv,hv
2022-01-21T03:20:50.040Z,36.0256667,-117.8198333,1.66,0.59,ml,12,90,0.044,0.1,ci,ci39919135,2022-01-21T17:16:53.669Z,"12km E of Coso Junction, CA",earthquake,0.15,0.23,0.125,4,reviewed,ci,ci
2022-01-21T03:03:55.230Z,19.173999786377,-155.468994140625,31.9099998474121,1.84000003,md,37,95,,0.119999997,hv,hv72883827,2022-01-21T03:07:11.730Z,"3 km SSE of Pāhala, Hawaii",earthquake,0.55,0.810000002,1.40999997,10,automatic,hv,hv
2022-01-21T03:01:48.780Z,38.831665,-122.8118362,1.68,0.85,md,11,94,0.008372,0.01,nc,nc73681301,2022-01-21T03:03:24.236Z,"8km NW of The Geysers, CA",earthquake,0.33,0.86,,1,automatic,nc,nc
2022-01-21T02:58:41.170Z,32.942,-115.5218333,8.11,1.48,ml,25,56,0.05199,0.19,ci,ci39919127,2022-01-21T18:40:37.420Z,"4km S of Brawley, CA",earthquake,0.24,0.71,0.221,21,reviewed,ci,ci
2022-01-21T02:49:04.270Z,35.9003333,-117.6908333,4.66,1.21,ml,28,47,0.05772,0.08,ci,ci39919111,2022-01-21T18:31:31.240Z,"20km ESE of Little Lake, CA",earthquake,0.1,0.23,0.115,17,reviewed,ci,ci
2022-01-21T02:48:15.260Z,38.831665,-122.8160019,1.55,0.36,md,9,79,0.009467,0.01,nc,nc73681296,2022-01-21T02:49:52.681Z,"8km NW of The Geysers, CA",earthquake,0.55,1.48,,1,automatic,nc,nc
2022-01-21T02:46:50.250Z,17.9501,-66.7445,13,1.64,md,3,331,0.137,0.15,pr,pr2022021013,2022-01-22T04:31:08.397Z,"5 km SSW of Tallaboa, Puerto Rico",earthquake,1.85,0.56,0.15,3,reviewed,pr,pr
2022-01-21T02:36:27.320Z,17.9665,-67.0983,13,1.99,md,3,259,0.0415,0.08,pr,pr2022021019,2022-01-22T04:30:29.254Z,"5 km W of La Parguera, Puerto Rico",earthquake,1.41,0.86,0.05,2,reviewed,pr,pr
2022-01-21T02:34:41.350Z,19.1971666666667,-155.696833333333,0.07,2.25,md,43,65,,0.2,hv,hv72883802,2022-01-21T03:30:44.080Z,"15 km NNE of Hawaiian Ocean View, Hawaii",earthquake,0.31,0.33,0.198686895258408,21,reviewed,hv,hv
2022-01-21T02:30:21.680Z,17.985,-67.0216,10,1.99,md,3,276,0.0275,0.04,pr,pr2022021018,2022-01-22T04:29:35.917Z,"2 km ENE of La Parguera, Puerto Rico",earthquake,1.18,0.81,0,1,reviewed,pr,pr
2022-01-21T02:28:40.710Z,17.9733,-66.9115,16,2.04,md,4,183,0.0323,0.06,pr,pr2022021017,2022-01-22T04:28:23.261Z,"0 km WNW of Guánica, Puerto Rico",earthquake,1.64,0.86,0.07,3,reviewed,pr,pr
2022-01-21T02:25:43.840Z,17.9898,-66.851,17,1.47,md,4,319,0.0318,0.13,pr,pr2022021016,2022-01-22T04:27:56.909Z,"3 km W of Indios, Puerto Rico",earthquake,4.46,1.27,0.27,2,reviewed,pr,pr
2022-01-21T02:12:47.140Z,17.7116,-67.7013,12,3.24,md,7,225,0.6611,0.1,pr,pr2022021015,2022-01-22T04:25:56.173Z,"61 km WSW of Pole Ojea, Puerto Rico",earthquake,2.11,1.53,0.05,5,reviewed,pr,pr
2022-01-21T02:08:01.500Z,39.4186667,-110.3006667,-2.44,1.67,md,7,199,0.01969,0.12,uu,uu60478362,2022-01-21T16:37:32.620Z,"16 km SSE of Sunnyside, Utah",earthquake,1.28,2.79,0.225,7,reviewed,uu,uu
2022-01-21T02:07:48.500Z,19.224666595459,-155.379333496094,32.4500007629395,2.23000002,md,45,154,,0.129999995,hv,hv72883757,2022-01-21T02:11:03.200Z,"10 km ENE of Pāhala, Hawaii",earthquake,0.56,0.639999986,0.790000021,28,automatic,hv,hv
2022-01-21T02:06:43.980Z,19.1459999084473,-155.499160766602,33.3600006103516,1.85000002,md,30,149,,0.150000006,hv,hv72883752,2022-01-21T02:09:54.070Z,"6 km SSW of Pāhala, Hawaii",earthquake,0.73,1.01999998,0.920000017,3,automatic,hv,hv
2022-01-21T02:05:30.010Z,46.1955,-122.188333333333,2.03,0.45,ml,13,89,0.004626,0.11,uw,uw61811956,2022-01-21T20:18:56.670Z,"Mount St. Helens area, Washington",earthquake,0.33,0.42,0.406330173854592,5,reviewed,uw,uw
2022-01-21T02:04:00.660Z,19.2311668395996,-155.392669677734,0.180000007152557,2.04,ml,21,203,,0.360000014,hv,hv72883742,2022-01-21T02:09:36.010Z,"9 km ENE of Pāhala, Hawaii",earthquake,1.92,15,4.21,3,automatic,hv,hv
2022-01-21T02:03:54.820Z,19.2224998474121,-155.393005371094,32.0200004577637,2.19,ml,45,150,,0.150000006,hv,hv72883747,2022-01-21T02:09:42.020Z,"9 km ENE of Pāhala, Hawaii",earthquake,0.5,0.819999993,2.77,7,automatic,hv,hv
2022-01-21T02:02:01.455Z,39.2486,-120.1202,9.5,0.6,ml,9,69.1,0.041,0.1397,nn,nn00832158,2022-01-21T23:08:30.579Z,"4 km NW of Carnelian Bay, California",earthquake,,1.3,0.26,7,reviewed,nn,nn
2022-01-21T02:01:32.670Z,19.4838333333333,-155.6505,4.42,2.37,ml,27,96,,0.11,hv,hv72883737,2022-01-21T02:22:10.990Z,"22 km E of Honaunau-Napoopoo, Hawaii",earthquake,0.31,0.52,0.163751556729392,15,reviewed,hv,hv
2022-01-21T01:58:40.030Z,61.5794,-148.0916,18.7,1.1,ml,,,,0.23,ak,ak022yr88lf,2022-01-21T02:01:45.503Z,"31 km SE of Chickaloon, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-21T01:48:08.020Z,17.8748,-66.8883,13,1.96,md,3,298,0.1007,0.07,pr,pr2022021014,2022-01-22T04:24:30.365Z,"10 km S of Guánica, Puerto Rico",earthquake,3.74,4.15,0.05,2,reviewed,pr,pr
2022-01-21T01:45:52.830Z,38.8326683,-122.8154984,1.75,0.71,md,20,53,0.01018,0.02,nc,nc73681286,2022-01-21T01:47:28.916Z,"8km NW of The Geysers, CA",earthquake,0.22,0.43,0.14,2,automatic,nc,nc
2022-01-21T01:37:51.610Z,35.6748333,-117.5591667,9.65,1.08,ml,21,87,0.0875,0.15,ci,ci39919095,2022-01-21T18:25:51.656Z,"12km ENE of Ridgecrest, CA",earthquake,0.22,0.63,0.111,13,reviewed,ci,ci
2022-01-21T01:29:37.770Z,19.4853333333333,-155.648666666667,4.35,0.85,md,15,94,,0.09,hv,hv72883707,2022-01-21T02:09:06.320Z,"22 km E of Honaunau-Napoopoo, Hawaii",earthquake,0.33,0.67,0.0921623382123083,4,reviewed,hv,hv
2022-01-21T01:24:45.750Z,17.9998,-66.8446,14,2.11,md,6,155,0.0425,0.1,pr,pr2022021012,2022-01-22T04:22:28.293Z,"2 km WNW of Indios, Puerto Rico",earthquake,0.59,0.55,0.18,6,reviewed,pr,pr
2022-01-21T01:22:42.150Z,17.9896,-66.8383,12,2.79,md,16,156,0.0434,0.15,pr,pr2022021000,2022-01-21T02:31:41.858Z,"2 km WSW of Indios, Puerto Rico",earthquake,0.57,0.38,0.3,7,reviewed,pr,pr
2022-01-21T01:22:08.650Z,37.8806667,-112.9126667,6.95,1.52,ml,11,191,0.2341,0.09,uu,uu60029874,2022-01-21T16:35:26.800Z,"8 km WNW of Parowan, Utah",earthquake,0.94,1.79,0.071,8,reviewed,uu,uu
2022-01-21T01:21:44.970Z,41.7083333,-112.4085,2.74,0.3,md,5,100,0.1678,0.1,uu,uu60478357,2022-01-21T16:25:39.230Z,"9 km W of Thatcher, Utah",earthquake,0.84,31.61,0.173,4,reviewed,uu,uu
2022-01-21T01:20:37.810Z,38.7994995,-122.7845001,3.32,0.35,md,8,82,0.01195,0.01,nc,nc73681276,2022-01-21T01:22:15.145Z,"4km NW of The Geysers, CA",earthquake,0.62,1.63,,1,automatic,nc,nc
2022-01-21T01:14:41.600Z,17.8483,-66.9075,6,2.18,md,6,294,0.1299,0.11,pr,pr2022021011,2022-01-22T04:21:53.261Z,"13 km S of Guánica, Puerto Rico",earthquake,0.71,0.34,0.12,6,reviewed,pr,pr
2022-01-21T01:06:56.360Z,33.9213333,-116.8178333,8.37,0.6,ml,21,85,0.08916,0.09,ci,ci39919087,2022-01-21T20:03:38.549Z,"3km W of Cabazon, CA",earthquake,0.21,0.61,0.149,14,reviewed,ci,ci
2022-01-21T01:03:14.830Z,17.8503,-66.9078,6,1.89,md,4,297,0.128,0.05,pr,pr2022021010,2022-01-22T04:20:55.957Z,"13 km S of Guánica, Puerto Rico",earthquake,0.69,0.33,0.04,4,reviewed,pr,pr
2022-01-21T01:01:04.980Z,39.4205,-110.3095,-1.59,1.67,md,7,196,0.01261,0.13,uu,uu60478352,2022-01-21T16:20:27.930Z,"16 km SSE of Sunnyside, Utah",earthquake,1.2,0.78,0.115,7,reviewed,uu,uu
2022-01-21T00:57:22.470Z,19.2186660766602,-155.423828125,32.4799995422363,2.36,ml,44,134,,0.119999997,hv,hv72883657,2022-01-21T01:14:25.040Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.52,0.720000029,2.75,17,automatic,hv,hv
2022-01-21T00:55:37.230Z,34.4483333,-117.9425,11.73,0.28,ml,5,130,0.01069,0.04,ci,ci39919063,2022-01-21T01:08:26.803Z,"7km SSW of Pearblossom, CA",earthquake,0.36,0.42,0.162,3,reviewed,ci,ci
2022-01-21T00:54:29.630Z,33.4538333,-116.5355,10.64,0.24,ml,15,93,0.06906,0.1,ci,ci39919071,2022-01-21T20:01:20.098Z,"17km SE of Anza, CA",earthquake,0.27,0.48,0.047,7,reviewed,ci,ci
2022-01-21T00:53:39.210Z,34.447,-117.9451667,11.84,0.1,ml,5,129,0.008684,0.05,ci,ci39919055,2022-01-21T01:04:08.463Z,"7km SSW of Pearblossom, CA",earthquake,0.35,0.49,0.238,3,reviewed,ci,ci
2022-01-21T00:49:27.920Z,17.852,-66.9118,6,2.76,md,19,249,0.1273,0.2,pr,pr2022021009,2022-01-22T04:19:16.605Z,"13 km S of Guánica, Puerto Rico",earthquake,0.58,0.36,0.33,16,reviewed,pr,pr
2022-01-21T00:46:23.560Z,35.5926667,-117.4826667,5.93,1.42,ml,27,82,0.01778,0.16,ci,ci39919039,2022-01-21T01:23:43.310Z,"18km E of Ridgecrest, CA",earthquake,0.25,0.42,0.184,16,reviewed,ci,ci
2022-01-21T00:43:46.534Z,65.0362,-147.1025,1.1,1.2,ml,,,,0.66,ak,ak022yqjlr1,2022-01-21T00:46:57.462Z,"18 km N of Two Rivers, Alaska",earthquake,,3.5,,,automatic,ak,ak
2022-01-21T00:38:20.110Z,19.3419990539551,-155.191497802734,2.86999988555908,1.92,ml,32,75,,0.230000004,hv,hv72883632,2022-01-21T00:43:59.890Z,"12 km SSE of Volcano, Hawaii",earthquake,0.46,1.21000004,3.56,4,automatic,hv,hv
2022-01-21T00:37:22.580Z,34.0111667,-117.1188333,8.93,1.16,ml,40,87,0.02482,0.18,ci,ci39919015,2022-01-21T01:01:36.469Z,"7km WNW of Calimesa, CA",earthquake,0.19,0.51,0.19,23,reviewed,ci,ci
2022-01-21T00:30:19.730Z,33.3063333,-116.325,12.38,1.13,ml,46,112,0.04073,0.2,ci,ci39919007,2022-01-21T19:59:33.437Z,"7km NE of Borrego Springs, CA",earthquake,0.24,0.46,0.128,23,reviewed,ci,ci
2022-01-21T00:25:35.440Z,35.8365,-117.6765,8.06,0.88,ml,22,37,0.06745,0.13,ci,ci39918999,2022-01-21T01:14:35.349Z,"24km ESE of Little Lake, CA",earthquake,0.2,0.45,0.086,10,reviewed,ci,ci
2022-01-21T00:22:27.860Z,17.9415,-66.8591,17,1.5,md,3,309,0.0392,0.05,pr,pr2022021008,2022-01-22T04:18:48.414Z,"5 km SE of Maria Antonia, Puerto Rico",earthquake,3.68,0.74,0.09,3,reviewed,pr,pr
2022-01-21T00:20:42.110Z,19.220832824707,-155.417495727539,33.6100006103516,1.91,ml,48,138,,0.129999995,hv,hv72883622,2022-01-21T00:26:13.230Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.48,0.670000017,4.59,5,automatic,hv,hv
2022-01-21T00:20:06.290Z,49.4208333333333,-120.537333333333,-0.51,1.73,ml,5,223,0.6042,0.15,uw,uw61811946,2022-01-21T20:43:56.200Z,"4 km SSW of Princeton, Canada",explosion,2.29,31.61,0.0483199829728566,2,reviewed,uw,uw
2022-01-21T00:11:12.093Z,60.636,-146.7705,12.1,2.3,ml,,,,0.71,ak,ak022yqco8j,2022-01-21T00:16:03.753Z,"25 km S of Tatitlek, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-21T00:07:16.670Z,46.1913333333333,-122.1935,-0.62,0.27,mh,6,130,0.008646,0.03,uw,uw61811936,2022-01-21T20:39:59.080Z,"36 km NNE of Amboy, Washington",earthquake,0.34,1.04,,0,reviewed,uw,uw
2022-01-21T00:05:30.140Z,37.4665,-118.8403333,3.9,0.68,md,13,218,0.1236,0.03,nc,nc73681266,2022-01-21T00:20:32.299Z,"18km SW of Toms Place, CA",earthquake,1.01,3.44,0.11,10,reviewed,nc,nc
2022-01-21T00:04:55.180Z,17.9278,-67.0908,10,0.97,md,3,302,0.0625,0.02,pr,pr2022021007,2022-01-22T04:18:07.574Z,"7 km SW of La Parguera, Puerto Rico",earthquake,0.91,0.93,0.27,3,reviewed,pr,pr
2022-01-20T23:59:36.663Z,44.0575,148.0745,38.31,5.2,mb,,132,3.949,0.82,us,us7000gdps,2022-01-21T00:15:06.040Z,"112 km ENE of Shikotan, Russia",earthquake,9.3,6.9,0.023,618,reviewed,us,us
2022-01-20T23:52:51.210Z,43.5266667,-111.1093333,6.2,1.35,ml,11,217,0.117,0.14,mb,mb80536509,2022-01-21T15:27:39.780Z,"8 km S of Victor, Idaho",earthquake,0.99,1.17,0.221,8,reviewed,mb,mb
2022-01-20T23:52:20.150Z,38.7898331,-122.7626648,1.19,0.53,md,11,81,0.01102,0.04,nc,nc73681261,2022-01-20T23:53:59.671Z,"2km NNW of The Geysers, CA",earthquake,0.33,0.68,0.38,2,automatic,nc,nc
2022-01-20T23:51:42.740Z,35.13883333,-95.569,1.68,1.45,ml,48,94,0.1034796938,0.29,ok,ok2022bknu,2022-01-21T14:27:58.213Z,"8 km ESE of Canadian, Oklahoma",earthquake,,1.4,0.23,13,reviewed,ok,ok
2022-01-20T23:43:39.770Z,19.4875,-155.648666666667,4.76,0.71,md,14,102,,0.09,hv,hv72883587,2022-01-21T01:58:17.600Z,"Island of Hawaii, Hawaii",earthquake,0.33,0.66,0.130263224751712,4,reviewed,hv,hv
2022-01-20T23:43:20.220Z,60.0145,-153.084166666667,1.89,-0.76,ml,4,149,,0.02,av,av91468671,2022-01-21T18:45:55.180Z,"62 km ENE of Pedro Bay, Alaska",earthquake,0.3,1.73,0.0927610311669815,4,reviewed,av,av
2022-01-20T23:40:46.420Z,44.3713333,-110.3883333,8,0.19,md,11,129,0.07688,0.13,uu,uu60478327,2022-01-21T15:17:45.560Z,"65 km ESE of West Yellowstone, Montana",earthquake,0.41,0.62,0.183,5,reviewed,uu,uu
2022-01-20T23:35:54.110Z,38.5373333,-119.5316667,3.55,2.51,md,17,83,0.04659,0.06,nc,nc73681251,2022-01-21T07:48:10.962Z,"5km WNW of Walker, CA",earthquake,0.25,0.33,0.268,54,reviewed,nc,nc
2022-01-20T23:33:52.506Z,-20.4834,-175.4169,10,4.7,mb,,100,6.747,0.71,us,us7000gdpt,2022-01-21T00:36:19.040Z,"76 km NNW of Nuku‘alofa, Tonga",earthquake,16,1.9,0.115,23,reviewed,us,us
2022-01-20T23:30:50.023Z,44.4552,-115.2038,10,2.8,ml,,62,0.849,1.02,us,us7000gdpj,2022-01-21T05:04:58.394Z,"33 km NW of Stanley, Idaho",earthquake,2,2,0.041,78,reviewed,us,us
2022-01-20T23:28:17.302Z,61.084,-150.7128,52,1.6,ml,,,,1.71,ak,ak022xgly6a,2022-01-20T23:32:18.907Z,"17 km N of Point Possession, Alaska",earthquake,,1.3,,,automatic,ak,ak
2022-01-20T23:28:00.160Z,34.0468333,-117.2356667,14.53,0.89,ml,20,144,0.1277,0.11,ci,ci39918967,2022-01-21T00:54:19.078Z,"2km E of Loma Linda, CA",earthquake,0.33,0.65,0.122,13,reviewed,ci,ci
2022-01-20T23:27:59.670Z,32.5876667,-117.0081667,-0.34,1.58,ml,34,208,0.06879,0.23,ci,ci39918959,2022-01-21T01:19:14.250Z,"5km NE of San Ysidro, CA",quarry blast,1.37,31.61,0.149,15,reviewed,ci,ci
2022-01-20T23:03:54.780Z,38.833,-122.8165,2.02,0.48,md,15,61,0.01082,0.03,nc,nc71127074,2022-01-21T00:11:31.742Z,"8km NW of The Geysers, CA",earthquake,0.2,0.22,0.079,2,reviewed,nc,nc
2022-01-20T23:03:41.220Z,38.8298333,-122.8148333,2.47,-0.11,md,10,99,0.007426,0.04,nc,nc73681246,2022-01-21T00:08:31.896Z,"8km NW of The Geysers, CA",earthquake,0.24,0.43,,1,reviewed,nc,nc
2022-01-20T22:57:46.180Z,48.0906666666667,-121.943,-0.4,1.58,ml,14,72,0.01316,0.11,uw,uw61811916,2022-01-20T23:39:45.011Z,"2 km ENE of Granite Falls, Washington",explosion,0.31,31.61,0.162698969184387,8,reviewed,uw,uw
2022-01-20T22:54:05.490Z,35.8763333,-117.6903333,5,0.93,ml,22,78,0.07844,0.08,ci,ci39918887,2022-01-21T01:11:39.204Z,"21km ESE of Little Lake, CA",earthquake,0.11,0.26,0.111,11,reviewed,ci,ci
2022-01-20T22:53:12.200Z,46.1966666666667,-122.185,1.93,0.48,ml,13,87,0.003551,0.1,uw,uw61811911,2022-01-21T01:52:11.330Z,"37 km NNE of Amboy, Washington",earthquake,0.33,0.41,0.16257407644108,5,reviewed,uw,uw
2022-01-20T22:51:42.300Z,19.242000579834,-155.462661743164,32.0200004577637,1.75,md,30,97,,0.119999997,hv,hv72883527,2022-01-20T22:54:52.270Z,"4 km NNE of Pāhala, Hawaii",earthquake,0.59,0.74000001,0.579999983,3,automatic,hv,hv
2022-01-20T22:37:19.120Z,35.8618333,-117.6835,10.73,0.17,ml,7,86,0.08365,0.08,ci,ci39918863,2022-01-20T23:09:34.414Z,"22km ESE of Little Lake, CA",earthquake,0.3,1.01,0.077,3,reviewed,ci,ci
2022-01-20T22:31:02.860Z,33.993,-116.6755,16.37,1.1,ml,33,73,0.05085,0.08,ci,ci39918855,2022-01-21T00:46:30.120Z,"11km SW of Morongo Valley, CA",earthquake,0.16,0.4,0.093,18,reviewed,ci,ci
2022-01-20T22:17:01.570Z,33.0635,-115.0013333,-0.25,1.57,ml,13,84,0.0931,0.3,ci,ci39918839,2022-01-21T19:52:55.478Z,"45km NE of Holtville, CA",quarry blast,0.87,31.61,0.116,7,reviewed,ci,ci
2022-01-20T22:16:09.110Z,38.800499,-122.7558365,0.66,0.86,md,15,96,0.003031,0.04,nc,nc73681236,2022-01-20T22:17:43.789Z,"3km N of The Geysers, CA",earthquake,0.24,0.47,0.01,3,automatic,nc,nc
2022-01-20T22:09:39.772Z,61.9149,-152.9204,2.5,0.9,ml,,,,0.72,ak,ak022xfwge1,2022-01-20T22:28:01.778Z,"80 km W of Skwentna, Alaska",earthquake,,0.3,,,reviewed,ak,ak
2022-01-20T22:05:59.233Z,63.363,-149.9606,84.1,1.5,ml,,,,0.56,ak,ak022xfvoc4,2022-01-20T22:10:49.794Z,"50 km W of Cantwell, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-20T22:05:12.280Z,38.7874985,-122.7444992,1.61,0.73,md,11,84,0.007418,0.02,nc,nc73681231,2022-01-20T22:06:47.991Z,"2km NE of The Geysers, CA",earthquake,0.32,0.67,0.15,2,automatic,nc,nc
2022-01-20T22:02:02.410Z,39.4251667,-110.3173333,-1.27,1.35,md,6,193,0.006109,0.03,uu,uu60478312,2022-01-21T15:52:40.460Z,"15 km SSE of Sunnyside, Utah",earthquake,1,0.23,0.14,5,reviewed,uu,uu
2022-01-20T21:57:56.590Z,38.8026657,-122.8081665,2.3,0.35,md,11,83,0.01136,0.02,nc,nc73681221,2022-01-20T21:59:32.976Z,"5km WNW of The Geysers, CA",earthquake,0.41,0.7,,1,automatic,nc,nc
2022-01-20T21:55:23.930Z,35.9141667,-117.4606667,1.77,1.1,ml,19,122,0.1165,0.12,ci,ci39918815,2022-01-21T00:41:29.265Z,"17km NNW of Searles Valley, CA",earthquake,0.23,0.29,0.086,11,reviewed,ci,ci
2022-01-20T21:51:03.770Z,38.7996674,-122.8095016,2.51,2.11,md,38,107,0.01239,0.07,nc,nc73681211,2022-01-20T22:40:10.800Z,"5km WNW of The Geysers, CA",earthquake,0.21,0.38,0.23,18,automatic,nc,nc
2022-01-20T21:49:06.153Z,-3.6688,130.9338,10,4.6,mb,,73,1.509,1.18,us,us7000gdnq,2022-01-20T22:01:33.040Z,"226 km E of Amahai, Indonesia",earthquake,4.8,1.9,0.112,24,reviewed,us,us
2022-01-20T21:47:43.140Z,34.4471667,-117.9511667,11.15,1.41,ml,31,36,0.003928,0.16,ci,ci39918807,2022-01-21T00:34:22.630Z,"8km SSW of Pearblossom, CA",earthquake,0.18,0.36,0.129,19,reviewed,ci,ci
2022-01-20T21:44:44.040Z,33.502,-116.4503333,5.94,1.31,ml,55,71,0.02965,0.18,ci,ci39918783,2022-01-20T22:03:15.910Z,"22km ESE of Anza, CA",earthquake,0.17,0.36,0.131,34,reviewed,ci,ci
2022-01-20T21:37:32.560Z,38.7905,-122.7618333,2.31,-0.1,md,16,63,0.01025,0.03,nc,nc73681206,2022-01-20T23:26:57.493Z,"2km NNW of The Geysers, CA",earthquake,0.24,0.46,0.059,3,reviewed,nc,nc
2022-01-20T21:32:07.754Z,36.7062,-116.3522,6.7,-0.3,ml,10,181.15,0.029,0.0809,nn,nn00832110,2022-01-21T02:37:42.359Z,"42 km ESE of Beatty, Nevada",earthquake,,2.4,0.08,3,reviewed,nn,nn
2022-01-20T21:29:47.660Z,35.9145,-117.717,2.67,0.46,ml,13,58,0.06352,0.1,ci,ci39918759,2022-01-20T21:49:13.936Z,"17km E of Little Lake, CA",earthquake,0.19,0.28,0.14,4,reviewed,ci,ci
2022-01-20T21:25:34.620Z,62.5426,-155.9028,0,1.7,ml,,,,0.73,ak,ak022xfehbu,2022-01-20T21:38:56.302Z,"48 km SSW of McGrath, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-20T21:19:13.990Z,19.1981658935547,-155.477828979492,31.3600006103516,2.11999989,md,40,85,,0.109999999,hv,hv72883432,2022-01-20T21:22:30.230Z,"0 km S of Pāhala, Hawaii",earthquake,0.52,0.680000007,0.810000002,19,automatic,hv,hv
2022-01-20T21:15:52.770Z,38.8391685,-122.7558365,0.81,0.87,md,13,177,0.01401,0.04,nc,nc73681201,2022-01-20T21:17:30.206Z,"3km NW of Cobb, CA",earthquake,0.41,0.62,,2,automatic,nc,nc
2022-01-20T21:06:28.030Z,19.4233341217041,-155.276992797852,0.660000026226044,1.75,ml,13,139,,0.25,hv,hv72883422,2022-01-20T21:11:59.800Z,"5 km WSW of Volcano, Hawaii",earthquake,0.43,0.230000004,0.28,7,automatic,hv,hv
2022-01-20T21:02:16.020Z,34.0613333,-118.87,11.17,1.89,ml,40,81,0.07948,0.24,ci,ci39918727,2022-01-20T21:32:48.844Z,"8km NW of Malibu, CA",earthquake,0.34,0.51,0.178,19,reviewed,ci,ci
2022-01-20T20:58:41.960Z,35.7518333,-117.5698333,6.61,0.83,ml,16,144,0.06762,0.1,ci,ci39918719,2022-01-20T21:24:48.797Z,"15km W of Searles Valley, CA",earthquake,0.25,0.45,0.129,9,reviewed,ci,ci
2022-01-20T20:57:23.820Z,44.4185,-122.7705,10.79,1.39,ml,10,78,0.1075,0.19,uw,uw61803087,2022-01-21T21:02:10.550Z,"3 km NW of Sweet Home, Oregon",earthquake,0.4,1.3,0.120325031031146,7,reviewed,uw,uw
2022-01-20T20:56:53.330Z,19.17799949646,-155.513336181641,33.7200012207031,2.01999998,md,41,102,,0.129999995,hv,hv72883392,2022-01-20T21:00:15.980Z,"4 km SW of Pāhala, Hawaii",earthquake,0.55,0.910000026,1.63999999,14,automatic,hv,hv
2022-01-20T20:50:10.540Z,38.8465004,-122.8166656,1.54,1.18,md,19,58,0.009676,0.03,nc,nc73681196,2022-01-20T21:57:10.547Z,"8km WNW of Cobb, CA",earthquake,0.21,0.47,0.01,3,automatic,nc,nc
2022-01-20T20:44:38.420Z,39.4241667,-110.313,-1.5,1.99,md,7,194,0.009372,0.07,uu,uu60478297,2022-01-20T21:21:10.130Z,"15 km SSE of Sunnyside, Utah",earthquake,0.71,0.3,0.235,7,reviewed,uu,uu
2022-01-20T20:42:58.690Z,33.4993333,-116.5015,10.88,0.48,ml,20,64,0.06303,0.13,ci,ci39918687,2022-01-20T21:24:27.263Z,"17km ESE of Anza, CA",earthquake,0.26,0.47,0.225,2,reviewed,ci,ci
2022-01-20T20:39:56.246Z,63.0807,-150.9747,121.6,1.8,ml,,,,0.28,ak,ak022xew38u,2022-01-20T20:46:39.822Z,"63 km SE of Denali National Park, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-20T20:28:49.710Z,49.1366666666667,-122.154166666667,-0.71,0.96,md,6,202,0.3902,0.27,uw,uw61803082,2022-01-21T20:56:58.330Z,"10 km E of Mission, Canada",explosion,2.26,31.61,0.062479358714306,3,reviewed,uw,uw
2022-01-20T20:24:31.830Z,33.5868333,-116.8106667,7.13,1.92,ml,67,22,0.03947,0.17,ci,ci39918679,2022-01-20T21:22:51.150Z,"13km WNW of Anza, CA",earthquake,0.14,0.38,0.193,25,reviewed,ci,ci
2022-01-20T20:19:00.710Z,36.4706667,-117.983,7.83,0.93,ml,6,172,0.08414,0.24,ci,ci39918671,2022-01-20T21:28:04.815Z,"15km SSE of Lone Pine, CA",earthquake,1.34,3.06,0.054,2,reviewed,ci,ci
2022-01-20T20:14:42.954Z,68.8216,-144.5159,28.7,2.9,ml,,,,0.8,ak,ak022xequis,2022-01-20T22:20:32.040Z,"88 km NNE of Arctic Village, Alaska",earthquake,,0.9,,,reviewed,ak,ak
2022-01-20T20:08:03.990Z,32.5738333,-117.1921667,16.19,0.85,ml,14,279,0.1361,0.19,ci,ci39918639,2022-01-20T21:17:02.294Z,"8km W of Imperial Beach, CA",earthquake,1.3,1.07,0.056,3,reviewed,ci,ci
2022-01-20T20:06:51.970Z,38.8073349,-122.8171692,2.89,0.84,md,15,76,0.009507,0.02,nc,nc73681176,2022-01-20T20:08:27.563Z,"6km WNW of The Geysers, CA",earthquake,0.32,0.69,,1,automatic,nc,nc
2022-01-20T20:06:32.191Z,63.7885,-147.1023,6.2,1.3,ml,,,,0.37,ak,ak022xeoyra,2022-01-20T20:13:35.965Z,"69 km SSW of Harding-Birch Lakes, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T20:06:06.080Z,38.8051682,-122.819664,2.79,0.58,md,14,69,0.008301,0.02,nc,nc73681171,2022-01-20T20:07:43.290Z,"6km WNW of The Geysers, CA",earthquake,0.35,0.7,0.44,2,automatic,nc,nc
2022-01-20T20:06:01.500Z,38.8074989,-122.8188324,3.08,1.41,md,12,79,0.008198,0.01,nc,nc73681166,2022-01-20T21:03:12.246Z,"6km WNW of The Geysers, CA",earthquake,0.4,1.09,,1,automatic,nc,nc
2022-01-20T20:05:30.967Z,-20.3512,-175.3802,10,4.8,mb,,205,6.73,0.84,us,us7000gdmq,2022-01-20T20:24:25.040Z,"89 km NNW of Nuku‘alofa, Tonga",earthquake,19.4,2,0.062,82,reviewed,us,us
2022-01-20T20:05:07.870Z,38.8061676,-122.8178329,2.95,1.43,md,30,66,0.009265,0.04,nc,nc73681161,2022-01-20T20:37:12.097Z,"6km WNW of The Geysers, CA",earthquake,0.23,0.41,0.04,5,automatic,nc,nc
2022-01-20T20:00:28.897Z,38.1958,-117.7579,4.3,1.5,ml,14,123.2,0.125,0.1345,nn,nn00832079,2022-01-20T20:04:08.128Z,"37 km SE of Mina, Nevada",earthquake,,0.9,0.33,9,automatic,nn,nn
2022-01-20T19:58:05.800Z,19.232666015625,-155.424835205078,34.060001373291,2.00999999,md,43,126,,0.119999997,hv,hv72883302,2022-01-20T20:01:30.260Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.61,0.779999971,1.12,24,automatic,hv,hv
2022-01-20T19:53:45.420Z,44.4418333,-114.1165,5.23,1.87,ml,14,66,0.081,0.29,mb,mb80536489,2022-01-20T22:17:01.220Z,"11 km SE of Challis, Idaho",earthquake,0.79,1.58,0.182,13,reviewed,mb,mb
2022-01-20T19:51:34.450Z,33.7398333,-116.8928333,4.16,0.73,ml,20,135,0.05861,0.1,ci,ci39918599,2022-01-20T21:09:58.704Z,"1km S of Valle Vista, CA",earthquake,0.24,0.42,0.131,13,reviewed,ci,ci
2022-01-20T19:50:30.432Z,61.6981,-151.9337,98.5,1.6,ml,,,,0.38,ak,ak022xecyip,2022-01-20T20:00:14.321Z,"43 km SW of Skwentna, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-20T19:42:14.950Z,39.4246667,-110.3163333,-1.55,2.03,ml,18,114,0.006814,0.15,uu,uu60478292,2022-01-20T20:11:20.220Z,"15 km SSE of Sunnyside, Utah",earthquake,0.48,0.18,0.084,4,reviewed,uu,uu
2022-01-20T19:41:32.220Z,38.8311667,-122.8191667,2.23,-0.16,md,9,71,0.01052,0.02,nc,nc71127069,2022-01-20T22:38:53.798Z,"8km NW of The Geysers, CA",earthquake,0.59,1.41,,1,reviewed,nc,nc
2022-01-20T19:40:58.830Z,38.7565,-122.7198333,2,0.18,md,11,102,0.006428,0.03,nc,nc73681156,2022-01-20T22:37:52.960Z,"3km SW of Anderson Springs, CA",earthquake,0.59,0.5,0.066,3,reviewed,nc,nc
2022-01-20T19:37:13.670Z,39.4236667,-110.317,-1.27,1.53,md,7,193,0.006289,0.08,uu,uu60478287,2022-01-20T20:30:22.160Z,"15 km SSE of Sunnyside, Utah",earthquake,0.58,0.18,0.269,7,reviewed,uu,uu
2022-01-20T19:35:48.120Z,19.41,-155.268666666667,2.33,0.85,md,17,51,,0.12,hv,hv72883272,2022-01-21T21:39:08.670Z,"5 km SW of Volcano, Hawaii",earthquake,0.21,0.27,0.163434083573524,3,reviewed,hv,hv
2022-01-20T19:35:27.282Z,38.1658,-117.8389,10,1,ml,9,173.76,0.099,0.0701,nn,nn00832078,2022-01-20T19:39:35.192Z,"34 km SE of Mina, Nevada",earthquake,,1.7,0.32,5,automatic,nn,nn
2022-01-20T19:27:26.730Z,19.3958339691162,-155.271499633789,3.15000009536743,1.75,md,17,79,,0.239999995,hv,hv72883252,2022-01-20T19:30:33.700Z,"6 km SW of Volcano, Hawaii",earthquake,0.44,0.540000021,0.870000005,8,automatic,hv,hv
2022-01-20T19:18:57.220Z,45.07,-111.7586667,-2,1.11,ml,8,141,0.258,0.2,mb,mb80536549,2022-01-21T15:55:33.440Z,"28 km SSE of Virginia City, Montana",quarry blast,1.09,31.61,0.175,6,reviewed,mb,mb
2022-01-20T19:17:45.110Z,38.836834,-122.8294983,2.44,0.76,md,15,128,0.004995,0.02,nc,nc73681146,2022-01-20T19:19:21.436Z,"9km NW of The Geysers, CA",earthquake,0.37,0.9,0.11,2,automatic,nc,nc
2022-01-20T19:16:47.064Z,38.1422,-117.9985,12.1,0.9,ml,10,140.1,0.031,0.0785,nn,nn00832074,2022-01-20T19:20:45.793Z,"29 km SSE of Mina, Nevada",earthquake,,0.5,0.3,5,automatic,nn,nn
2022-01-20T19:15:45.450Z,38.8330002,-122.8164978,1.69,0.85,md,13,85,0.01082,0.01,nc,nc73681141,2022-01-20T19:17:22.567Z,"8km NW of The Geysers, CA",earthquake,0.31,0.65,,1,automatic,nc,nc
2022-01-20T19:15:26.540Z,38.8301659,-122.8154984,1.83,1.8,md,26,44,0.007979,0.05,nc,nc73681136,2022-01-20T19:48:11.969Z,"8km NW of The Geysers, CA",earthquake,0.18,0.34,0.07,8,automatic,nc,nc
2022-01-20T19:13:52.321Z,-38.0844,176.653,145.76,4.6,mb,,85,0.589,1.51,us,us7000gdma,2022-01-22T01:16:45.234Z,"4 km WNW of Kawerau, New Zealand",earthquake,6.8,6.4,0.141,15,reviewed,us,us
2022-01-20T19:11:04.900Z,33.5235,-116.72,3.51,0.56,ml,31,36,0.04422,0.12,ci,ci39918543,2022-01-20T19:42:06.342Z,"6km SW of Anza, CA",earthquake,0.13,0.39,0.104,12,reviewed,ci,ci
2022-01-20T19:09:58.585Z,31.61722787,-104.3370925,7.057055663999999,2.5,ml,34,62,0.0821976969,0.3,tx,tx2022bkem,2022-01-22T00:39:28.040Z,"61 km WNW of Toyah, Texas",earthquake,1.00856988,1.003527629,0.2,18,reviewed,tx,tx
2022-01-20T19:09:08.059Z,15.8039,-94.9036,10,5,mww,,142,2.702,0.82,us,us7000gdm7,2022-01-21T06:55:50.233Z,"45 km S of San Mateo del Mar, Mexico",earthquake,6.8,1.9,0.068,21,reviewed,us,us
2022-01-20T19:07:31.800Z,44.3033333,-115.1646667,4.77,1.8,ml,10,82,0.812,0.15,mb,mb80536484,2022-01-20T22:24:53.760Z,"southern Idaho",earthquake,0.53,1.4,0.185,9,reviewed,mb,mb
2022-01-20T19:02:48.630Z,38.8231667,-122.803,2.87,0.55,md,5,114,0.00553,0.01,nc,nc73681131,2022-01-20T22:11:49.441Z,"6km NW of The Geysers, CA",earthquake,1.04,2.47,,1,reviewed,nc,nc
2022-01-20T19:02:12.910Z,38.8199997,-122.8073349,3.41,0.35,md,8,108,0.004009,0.02,nc,nc73681126,2022-01-20T19:03:46.348Z,"6km NW of The Geysers, CA",earthquake,0.6,1.68,,1,automatic,nc,nc
2022-01-20T19:01:18.290Z,33.9196667,-116.037,2.26,1.24,ml,29,150,0.08693,0.15,ci,ci39918503,2022-01-20T19:33:12.132Z,"24km S of Twentynine Palms, CA",earthquake,0.29,0.36,0.153,30,reviewed,ci,ci
2022-01-20T19:00:00.650Z,38.8303337,-122.8183365,2.3,0.85,md,14,61,0.009469,0.04,nc,nc73681121,2022-01-20T19:01:37.516Z,"8km NW of The Geysers, CA",earthquake,0.33,0.99,,1,automatic,nc,nc
2022-01-20T18:51:43.649Z,40.2255,-118.8429,14.6,1.5,ml,8,174.4,0.662,0.0898,nn,nn00832073,2022-01-20T18:55:17.074Z,"Nevada",earthquake,,1.4,0.16,4,automatic,nn,nn
2022-01-20T18:49:50.590Z,44.1098333333333,-123.052833333333,-0.55,1.07,ml,4,174,0.09975,0.06,uw,uw61803042,2022-01-21T20:49:47.590Z,"3 km SSE of Coburg, Oregon",explosion,0.4,31.61,0.177862867009624,3,reviewed,uw,uw
2022-01-20T18:41:52.930Z,38.1832,-117.7617,11.9,1.2,ml,10,165.11,0.114,0.0511,nn,nn00832070,2022-01-20T18:46:03.863Z,"38 km SE of Mina, Nevada",earthquake,,0.9,0.34,5,automatic,nn,nn
2022-01-20T18:32:25.930Z,19.2118339538574,-155.414169311523,32.9900016784668,2.02999997,md,37,151,,0.100000001,hv,hv72883172,2022-01-20T18:35:42.390Z,"6 km E of Pāhala, Hawaii",earthquake,0.58,0.75,1.63999999,6,automatic,hv,hv
2022-01-20T18:30:26.470Z,38.7993317,-122.8098297,1.8,1.11,md,27,70,0.01219,0.03,nc,nc73681111,2022-01-20T19:08:10.730Z,"5km WNW of The Geysers, CA",earthquake,0.19,0.33,0.09,4,automatic,nc,nc
2022-01-20T18:23:15.400Z,60.0271666666667,-153.052666666667,-0.49,-0.73,ml,4,132,,0.03,av,av91468471,2022-01-21T18:37:57.190Z,"64 km ENE of Pedro Bay, Alaska",earthquake,0.25,1.74,0.344453706574048,4,reviewed,av,av
2022-01-20T18:21:55.800Z,19.0251,-67.1846,10,3.36,md,21,224,0.5624,0.41,pr,pr2022020002,2022-01-22T01:05:36.040Z,"59 km N of San Antonio, Puerto Rico",earthquake,1.32,31.61,0.13,20,reviewed,pr,pr
2022-01-20T18:15:07.353Z,56.3515,-149.2229,10,3.1,ml,,223,2.329,0.62,us,us7000gdlw,2022-01-22T00:58:03.040Z,"232 km SE of Chiniak, Alaska",earthquake,8.3,2,0.053,46,reviewed,us,us
2022-01-20T18:11:21.570Z,37.3301667,-118.147,12.72,2.59,md,40,116,0.1471,0.08,nc,nc73681106,2022-01-22T00:48:30.040Z,"15km WSW of Deep Springs, CA",earthquake,0.33,0.44,0.212,44,reviewed,nc,nc
2022-01-20T18:11:08.102Z,31.71731302,-104.2759914,7.57121582,2.6,ml,37,58,0.04274072071,0.2,tx,tx2022bkco,2022-01-23T01:21:56.200Z,"51 km S of Whites City, New Mexico",earthquake,0.6211228747,0.540106661,0.1,19,reviewed,tx,tx
2022-01-20T17:51:29.633Z,61.9047,-150.7769,16.1,1.2,ml,,,,0.55,ak,ak022xd6ayr,2022-01-20T17:54:18.695Z,"33 km ESE of Skwentna, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-20T17:33:03.160Z,36.466,-117.9593333,9.05,1.37,ml,20,131,0.1008,0.13,ci,ci39918375,2022-01-20T19:26:54.028Z,"17km SE of Lone Pine, CA",earthquake,0.2,0.43,0.204,14,reviewed,ci,ci
2022-01-20T17:27:23.662Z,38.1803,-117.7621,12.4,1.3,ml,12,120.63,0.112,0.098,nn,nn00832064,2022-01-20T17:31:35.897Z,"38 km SE of Mina, Nevada",earthquake,,1.1,0.08,7,automatic,nn,nn
2022-01-20T17:23:30.403Z,53.0534,-170.6552,127.25,4.6,mb,,104,0.514,0.85,us,us7000gdkc,2022-01-22T00:20:55.040Z,"121 km W of Nikolski, Alaska",earthquake,7.3,6.6,0.031,304,reviewed,us,us
2022-01-20T17:21:55.527Z,57.7869,-153.5173,53.3,2.4,ml,,,,0.61,ak,ak022xczxgq,2022-01-20T17:33:25.801Z,"38 km WSW of Port Lions, Alaska",earthquake,,1.7,,,automatic,ak,ak
2022-01-20T17:10:03.615Z,-20.4535,-175.2501,10,4.8,mb,,124,6.881,0.73,us,us7000gdpe,2022-01-21T06:52:11.040Z,"76 km N of Nuku‘alofa, Tonga",earthquake,15,1.4,0.085,47,reviewed,us,us
2022-01-20T17:05:38.765Z,55.3076,-162.4868,161.01,3.4,ml,,133,0.7,0.9,us,us7000gdka,2022-01-20T18:58:30.040Z,"20 km NE of Cold Bay, Alaska",earthquake,13.9,11.2,0.097,14,reviewed,us,us
2022-01-20T17:04:43.960Z,19.1576671600342,-155.488494873047,34.3600006103516,1.87,md,34,209,,0.119999997,hv,hv72883077,2022-01-20T17:08:03.610Z,"5 km SSW of Pāhala, Hawaii",earthquake,1.26,0.930000007,1.84000003,6,automatic,hv,hv
2022-01-20T17:02:53.280Z,38.7833328,-122.7340012,1.63,1.05,md,16,81,0.002131,0.03,nc,nc73681101,2022-01-20T17:04:30.970Z,"2km ENE of The Geysers, CA",earthquake,0.27,0.55,0.16,2,automatic,nc,nc
2022-01-20T17:01:34.492Z,61.6774,-153.6869,0,1.5,ml,,,,0.49,ak,ak022xcvllk,2022-01-20T17:10:02.239Z,"99 km ENE of Lime Village, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-20T16:53:07.120Z,19.2361660003662,-155.410507202148,32.5900001525879,1.82000005,md,39,179,,0.109999999,hv,hv72883062,2022-01-20T16:56:03.420Z,"8 km ENE of Pāhala, Hawaii",earthquake,0.56,0.709999979,1.82000005,4,automatic,hv,hv
2022-01-20T16:52:08.489Z,38.1849,-117.7638,9.4,2.5,ml,20,93.88,0.117,0.1296,nn,nn00832058,2022-01-21T02:37:19.882Z,"37 km SE of Mina, Nevada",earthquake,,1.8,0.13,7,reviewed,nn,nn
2022-01-20T16:42:45.008Z,61.5672,-148.02,16.2,1.2,ml,,,,0.61,ak,ak022xciz3q,2022-01-20T16:47:19.213Z,"33 km SW of Glacier View, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-20T16:39:42.060Z,38.7926674,-122.745163,1.64,0.21,md,11,92,0.01387,0.02,nc,nc73681091,2022-01-20T16:41:16.215Z,"2km NNE of The Geysers, CA",earthquake,0.32,0.97,0.16,2,automatic,nc,nc
2022-01-20T16:38:55.789Z,38.1969,-117.745,0.9,1.6,ml,10,175.23,0.124,0.0617,nn,nn00832057,2022-01-20T16:43:05.471Z,"38 km SE of Mina, Nevada",earthquake,,9.7,0.21,6,automatic,nn,nn
2022-01-20T16:32:30.840Z,33.1595,-116.3923333,12.72,0.87,ml,25,68,0.09056,0.17,ci,ci39918319,2022-01-20T19:14:06.967Z,"11km S of Borrego Springs, CA",earthquake,0.3,0.65,0.103,13,reviewed,ci,ci
2022-01-20T16:25:27.200Z,38.8458328,-122.8213348,0.84,0.37,md,9,113,0.008954,0.01,nc,nc73681086,2022-01-20T16:27:05.405Z,"9km WNW of Cobb, CA",earthquake,0.27,0.85,,1,automatic,nc,nc
2022-01-20T16:21:01.441Z,38.1775,-117.8157,9.4,1.7,ml,18,109.4,0.12,0.1387,nn,nn00832055,2022-01-21T02:37:17.624Z,"34 km SE of Mina, Nevada",earthquake,,1.7,0.19,7,reviewed,nn,nn
2022-01-20T16:19:55.394Z,38.1852,-117.766,9.7,1.6,ml,18,121.05,0.118,0.1612,nn,nn00832053,2022-01-21T02:37:16.282Z,"37 km SE of Mina, Nevada",earthquake,,2,0.22,7,reviewed,nn,nn
2022-01-20T16:17:08.940Z,60.8879,-152.3647,117.4,1.8,ml,,,,0.59,ak,ak022xcdjed,2022-01-20T16:20:26.139Z,"62 km WNW of Nikiski, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-20T16:07:34.310Z,38.1859,-117.7552,11.4,1.3,ml,10,178.68,0.115,0.0946,nn,nn00832052,2022-01-20T16:11:34.244Z,"38 km SE of Mina, Nevada",earthquake,,2,0.33,6,automatic,nn,nn
2022-01-20T15:59:58.070Z,35.911,-117.6615,8.92,-0.36,ml,4,153,0.03791,0.15,ci,ci39918303,2022-01-20T17:27:26.109Z,"22km E of Little Lake, CA",earthquake,0.87,1.67,0.049,1,reviewed,ci,ci
2022-01-20T15:55:41.645Z,63.5698,-150.8642,0,1.8,ml,,,,0.92,ak,ak022xc0biz,2022-01-20T16:20:25.996Z,"42 km E of Denali National Park, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-20T15:50:56.309Z,59.4775,-152.4078,65.3,1.6,ml,,,,0.6,ak,ak022xbza1k,2022-01-20T16:03:33.828Z,"30 km WNW of Nanwalek, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-20T15:49:55.820Z,33.7381667,-116.8965,3.1,1.38,ml,40,74,0.05581,0.23,ci,ci39918295,2022-01-20T16:21:27.410Z,"1km SSW of Valle Vista, CA",earthquake,0.24,0.81,0.167,27,reviewed,ci,ci
2022-01-20T15:49:50.290Z,38.7900009,-122.7600021,1.69,0.36,md,8,109,0.01061,0.01,nc,nc73681081,2022-01-20T15:51:25.258Z,"1km NNW of The Geysers, CA",earthquake,0.41,0.76,,1,automatic,nc,nc
2022-01-20T15:49:10.630Z,39.4175,-110.2941667,-3.44,2,md,6,201,0.02485,0.11,uu,uu60478272,2022-01-20T16:49:46.710Z,"16 km SSE of Sunnyside, Utah",earthquake,1.38,3.44,0.32,6,reviewed,uu,uu
2022-01-20T15:45:32.340Z,38.833168,-122.8154984,1.59,0.36,md,13,62,0.01064,0.01,nc,nc73681071,2022-01-20T15:47:10.694Z,"8km NW of The Geysers, CA",earthquake,0.25,0.65,,1,automatic,nc,nc
2022-01-20T15:45:10.479Z,38.1827,-117.7655,9,3.4,mw,23,57.72,0.115,0.1234,nn,nn00832045,2022-01-21T22:13:56.088Z,"37 km SE of Mina, Nevada",earthquake,,1.4,,,reviewed,nn,nn
2022-01-20T15:44:11.690Z,38.5504,-119.5157,7,1.4,ml,15,114.51,0.036,0.1597,nn,nn00832046,2022-01-21T02:37:14.698Z,"1 km SSW of Coleville, California",earthquake,,1.1,0.22,6,reviewed,nn,nn
2022-01-20T15:35:35.390Z,46.3461666666667,-122.341333333333,12.97,1.06,ml,9,156,0.0682,0.1,uw,uw61802987,2022-01-20T19:03:05.380Z,"23 km SSE of Mossyrock, Washington",earthquake,0.53,0.67,0.043782258692571,6,reviewed,uw,uw
2022-01-20T15:33:08.932Z,-21.1888,-70.3062,35.86,4,mwr,,174,0.393,1.19,us,us7000gdjv,2022-01-20T20:47:46.377Z,"100 km N of Tocopilla, Chile",earthquake,3,13.3,0.058,29,reviewed,us,us
2022-01-20T15:27:38.620Z,48.4556666666667,-122.987833333333,21.07,0.55,md,11,89,0.06979,0.12,uw,uw61802982,2022-01-20T19:12:22.510Z,"9 km SSE of Friday Harbor, Washington",earthquake,0.51,0.72,0.192564490424201,8,reviewed,uw,uw
2022-01-20T15:23:19.000Z,36.588501,-121.1878357,5.46,1.31,md,7,139,0.01688,0.03,nc,nc73681061,2022-01-20T16:04:11.454Z,"8km NNW of Pinnacles, CA",earthquake,0.57,0.69,0.25,4,automatic,nc,nc
2022-01-20T15:15:46.950Z,33.597,-116.6268333,14.59,0.57,ml,17,71,0.02576,0.06,ci,ci39918263,2022-01-20T17:17:58.879Z,"6km NE of Anza, CA",earthquake,0.2,0.28,0.119,5,reviewed,ci,ci
2022-01-20T15:09:53.500Z,19.1838333333333,-155.386666666667,32.71,1.65,md,39,176,,0.1,hv,hv72882967,2022-01-20T20:34:39.740Z,"9 km ESE of Pāhala, Hawaii",earthquake,0.49,0.58,0.153107401935225,20,reviewed,hv,hv
2022-01-20T15:08:15.540Z,60.5261666666667,-152.706166666667,7.21,-0.59,ml,7,163,,0.06,av,av91468321,2022-01-21T17:58:08.280Z,"76 km W of Salamatof, Alaska",earthquake,0.41,0.65,0.14921219692736,7,reviewed,av,av
2022-01-20T15:04:18.730Z,38.8434982,-122.8198318,0.33,1.28,md,24,81,0.01317,0.07,nc,nc73681051,2022-01-20T15:37:12.329Z,"9km WNW of Cobb, CA",earthquake,0.22,0.48,0.08,4,automatic,nc,nc
2022-01-20T15:03:48.970Z,33.9221667,-116.044,2.41,1.33,ml,16,121,0.087,0.18,ci,ci39918223,2022-01-20T17:33:18.144Z,"24km S of Twentynine Palms, CA",earthquake,0.36,0.52,0.189,1,reviewed,ci,ci
2022-01-20T14:59:26.900Z,38.3576667,-111.1598333,5.88,1.57,md,8,219,0.5331,0.13,uu,uu60478262,2022-01-20T16:46:38.360Z,"23 km ENE of Torrey, Utah",earthquake,1.47,31.61,0.249,3,reviewed,uu,uu
2022-01-20T14:57:23.560Z,36.4658333,-117.959,9.47,1.52,ml,22,93,0.1011,0.13,ci,ci39918207,2022-01-20T17:15:47.039Z,"17km SE of Lone Pine, CA",earthquake,0.18,0.35,0.323,6,reviewed,ci,ci
2022-01-20T14:56:08.920Z,33.7485,-116.9015,9.82,0.44,ml,13,87,0.08112,0.1,ci,ci39918199,2022-01-20T16:40:54.818Z,"1km W of Valle Vista, CA",earthquake,0.36,0.66,0.031,6,reviewed,ci,ci
2022-01-20T14:55:31.100Z,33.5918333,-116.8061667,7.23,0.7,ml,27,43,0.03516,0.11,ci,ci39918191,2022-01-20T16:34:51.429Z,"13km WNW of Anza, CA",earthquake,0.15,0.36,0.169,15,reviewed,ci,ci
2022-01-20T14:51:35.302Z,61.4785,-147.3171,9.4,2.8,ml,,,,0.77,ak,ak022xbe0mh,2022-01-20T15:26:11.040Z,"40 km SSE of Glacier View, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-20T14:50:07.157Z,38.4979,-119.5237,6.6,1.1,ml,11,178.78,0.088,0.1223,nn,nn00832042,2022-01-20T14:54:15.212Z,"California-Nevada border region",earthquake,,0.9,0.2,7,automatic,nn,nn
2022-01-20T14:49:29.408Z,60.0867,-152.8161,88.5,1.3,ml,,,,0.5,ak,ak022xbdkp8,2022-01-20T14:55:04.962Z,"62 km WNW of Happy Valley, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T14:47:10.800Z,38.7985001,-122.7519989,2.3,0.94,md,14,96,0.00639,0.02,nc,nc73681046,2022-01-20T14:48:46.400Z,"2km N of The Geysers, CA",earthquake,0.3,0.7,0.2,3,automatic,nc,nc
2022-01-20T14:45:08.860Z,38.762001,-122.7180023,0.89,0.87,md,6,148,0.005378,0.02,nc,nc73681041,2022-01-20T14:46:46.100Z,"3km WSW of Anderson Springs, CA",earthquake,0.61,0.47,,2,automatic,nc,nc
2022-01-20T14:42:06.500Z,35.641,-117.5841667,1.64,-0.1,ml,4,233,0.1133,0.06,ci,ci39918151,2022-01-20T17:23:05.376Z,"9km ENE of Ridgecrest, CA",earthquake,1.03,0.58,0.046,1,reviewed,ci,ci
2022-01-20T14:38:10.070Z,38.8246651,-122.7975006,2.66,0.89,md,28,32,0.009903,0.03,nc,nc73681036,2022-01-20T14:39:46.221Z,"6km NW of The Geysers, CA",earthquake,0.21,0.42,0.13,4,automatic,nc,nc
2022-01-20T14:35:51.450Z,35.154,-118.1891667,10.29,0.79,ml,13,88,0.1415,0.08,ci,ci39918135,2022-01-20T17:09:37.581Z,"11km N of Mojave, CA",earthquake,0.16,0.44,0.161,7,reviewed,ci,ci
2022-01-20T14:34:21.890Z,35.0775,-119.0671667,12.46,1.23,ml,26,58,0.02328,0.19,ci,ci39918127,2022-01-20T18:38:29.702Z,"20km NW of Grapevine, CA",earthquake,0.28,1.05,0.093,7,reviewed,ci,ci
2022-01-20T14:21:20.098Z,38.6812,-97.4852,4.31,2.5,mb_lg,,118,0.738,0.41,us,us7000gdnm,2022-01-20T22:14:52.040Z,"5 km WSW of Gypsum, Kansas",earthquake,2.4,7.2,0.117,19,reviewed,us,us
2022-01-20T14:09:49.763Z,38.5408,-119.3939,3.8,1.4,ml,11,103.96,0.108,0.1311,nn,nn00832039,2022-01-20T14:13:15.209Z,"7 km ENE of Walker, California",earthquake,,5.4,0.02,3,automatic,nn,nn
2022-01-20T14:08:25.574Z,31.71513516,-104.4079225,6.131567383,2.3,ml,23,66,0.0918456085,0.3,tx,tx2022bjuo,2022-01-20T23:08:32.219Z,"51 km S of Whites City, New Mexico",earthquake,0.8957910203,1.011244886,0.2,13,reviewed,tx,tx
2022-01-20T14:06:53.620Z,35.0635,-118.3236667,5.76,0.59,ml,13,108,0.0742,0.07,ci,ci39918103,2022-01-20T18:27:36.807Z,"14km W of Mojave, CA",earthquake,0.17,0.53,0.159,6,reviewed,ci,ci
2022-01-20T14:01:45.910Z,19.3923333333333,-155.216166666667,3.17,1.96,ml,18,128,,0.17,hv,hv72882877,2022-01-20T20:45:24.380Z,"Island of Hawaii, Hawaii",earthquake,0.37,0.6,0.102609643138933,6,reviewed,hv,hv
2022-01-20T13:59:49.480Z,19.1981658935547,-155.451171875,35.3300018310547,1.92999995,md,38,121,,0.119999997,hv,hv72882872,2022-01-20T14:02:57.320Z,"2 km E of Pāhala, Hawaii",earthquake,0.5,0.709999979,0.379999995,5,automatic,hv,hv
2022-01-20T13:43:10.490Z,33.9353333,-117.2,13.31,1.67,ml,67,44,0.02562,0.19,ci,ci39918095,2022-01-20T16:20:25.700Z,"3km ENE of Moreno Valley, CA",earthquake,0.17,0.38,0.156,52,reviewed,ci,ci
2022-01-20T13:42:49.231Z,38.1224,-118.0597,8.1,0.5,ml,8,161.4,0.081,0.0623,nn,nn00832038,2022-01-20T13:46:52.343Z,"30 km S of Mina, Nevada",earthquake,,1.6,0.39,5,automatic,nn,nn
2022-01-20T13:40:20.888Z,63.2503,-150.6176,118.8,2.1,ml,,,,0.56,ak,ak022xaq6zr,2022-01-20T14:24:21.052Z,"64 km ESE of Denali National Park, Alaska",earthquake,,1.3,,,automatic,ak,ak
2022-01-20T13:37:29.730Z,44.0718333,-110.8548333,7.81,0.78,md,11,97,0.1122,0.12,uu,uu60478257,2022-01-20T14:30:38.680Z,"37 km E of Warm River, Idaho",earthquake,0.59,0.89,0.239,3,reviewed,uu,uu
2022-01-20T13:28:18.930Z,38.0633333,-118.7841667,5.5,1.14,md,19,135,0.2893,0.08,nc,nc73681031,2022-01-20T18:27:12.298Z,"26km SE of Bodie, CA",earthquake,0.5,8.24,0.254,16,reviewed,nc,nc
2022-01-20T13:23:23.998Z,38.1483,-118.0246,1.8,0.4,ml,8,177.05,0.052,0.1113,nn,nn00832036,2022-01-20T13:27:22.250Z,"27 km SSE of Mina, Nevada",earthquake,,5.4,0.18,3,automatic,nn,nn
2022-01-20T13:21:59.700Z,33.931,-117.1963333,12.14,0.81,ml,18,101,0.0255,0.2,ci,ci39918079,2022-01-20T14:27:04.609Z,"3km E of Moreno Valley, CA",earthquake,0.48,0.77,0.188,15,reviewed,ci,ci
2022-01-20T13:11:25.712Z,58.8825,-154.1297,129.8,2.2,ml,,,,0.32,ak,ak022xajzmi,2022-01-20T13:17:23.998Z,"72 km SSE of Kokhanok, Alaska",earthquake,,1.4,,,automatic,ak,ak
2022-01-20T13:10:43.980Z,33.4778333,-116.436,13.88,0.77,ml,30,77,0.1345,0.15,ci,ci39918063,2022-01-20T18:22:05.080Z,"24km ESE of Anza, CA",earthquake,0.21,0.51,0.103,13,reviewed,ci,ci
2022-01-20T13:09:32.490Z,38.8139992,-122.7626648,2.08,0.85,md,16,109,0.01355,0.02,nc,nc73681026,2022-01-20T13:11:09.192Z,"4km WSW of Cobb, CA",earthquake,0.27,0.57,0.21,3,automatic,nc,nc
2022-01-20T13:07:06.520Z,33.932,-117.1941667,12.36,0.64,ml,21,94,0.02348,0.13,ci,ci39918055,2022-01-20T18:05:36.347Z,"3km ENE of Moreno Valley, CA",earthquake,0.22,0.42,0.173,9,reviewed,ci,ci
2022-01-20T13:03:05.514Z,-30.6904,-178.0302,20.3,5.1,mb,,78,1.426,1.24,us,us7000gdin,2022-01-20T13:21:35.040Z,"Kermadec Islands, New Zealand",earthquake,8.6,5.3,0.05,130,reviewed,us,us
2022-01-20T12:59:42.190Z,37.5398333,-118.8226667,4.99,1.24,md,21,110,0.05037,0.03,nc,nc73681021,2022-01-20T22:24:10.692Z,"13km W of Toms Place, CA",earthquake,0.3,0.55,0.095,17,reviewed,nc,nc
2022-01-20T12:57:37.420Z,38.8231659,-122.7559967,1.74,0.85,md,9,226,0.01309,0.02,nc,nc73681016,2022-01-20T12:59:15.419Z,"3km W of Cobb, CA",earthquake,0.76,1.11,,1,automatic,nc,nc
2022-01-20T12:48:27.220Z,19.2098331451416,-155.3818359375,33.1100006103516,2.29,ml,47,158,,0.140000001,hv,hv72882787,2022-01-21T09:36:05.040Z,"10 km E of Pāhala, Hawaii",earthquake,0.55,0.610000014,3.35,17,automatic,hv,hv
2022-01-20T12:46:06.178Z,63.165,-144.3703,5.6,1.1,ml,,,,0.53,ak,ak022xa60kd,2022-01-20T12:51:00.897Z,"40 km NW of Mentasta Lake, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T12:34:28.600Z,44.2756667,-115.184,10.68,2.18,ml,11,83,0.904,0.28,mb,mb80536454,2022-01-20T16:13:39.460Z,"20 km WNW of Stanley, Idaho",earthquake,0.85,2.29,0.106,14,reviewed,mb,mb
2022-01-20T12:29:57.560Z,44.2801667,-115.1838333,10.98,2.42,ml,16,68,0.908,0.27,mb,mb80536449,2022-01-20T16:03:36.220Z,"20 km WNW of Stanley, Idaho",earthquake,0.58,1.88,0.111,14,reviewed,mb,mb
2022-01-20T12:23:13.318Z,60.1726,-152.4362,86.7,1.6,ml,,,,0.85,ak,ak022xa13mr,2022-01-20T12:28:08.063Z,"44 km WNW of Ninilchik, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-20T12:23:05.500Z,19.4048328399658,-155.251495361328,4.84000015258789,1.73,ml,11,111,,0.239999995,hv,hv72882767,2022-01-20T12:28:36.780Z,"4 km SSW of Volcano, Hawaii",earthquake,1.05,1.50999999,2.43,8,automatic,hv,hv
2022-01-20T12:21:48.817Z,60.0572,-151.655,64.1,1.6,ml,,,,0.61,ak,ak022xa0qpy,2022-01-20T12:32:18.709Z,"1 km NE of Ninilchik, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-20T12:19:39.650Z,33.4798333,-116.4461667,11.99,2.24,ml,74,30,0.0467,0.2,ci,ci39918023,2022-01-20T13:36:32.710Z,"23km ESE of Anza, CA",earthquake,0.2,0.42,0.166,26,reviewed,ci,ci
2022-01-20T12:10:59.820Z,38.7876663,-122.7695007,2.44,0.66,md,13,83,0.01503,0.03,nc,nc73681006,2022-01-20T12:12:34.426Z,"2km NW of The Geysers, CA",earthquake,0.32,0.67,0.51,3,automatic,nc,nc
2022-01-20T12:03:38.140Z,19.2115001678467,-155.419006347656,32.8499984741211,2.12,ml,47,143,,0.109999999,hv,hv72882742,2022-01-20T12:09:09.960Z,"6 km E of Pāhala, Hawaii",earthquake,0.54,0.660000026,2.16,11,automatic,hv,hv
2022-01-20T11:37:14.614Z,56.1221,-156.1818,47.5,3.4,ml,,,,0.53,ak,ak022x9intx,2022-01-20T18:05:50.846Z,"139 km E of Chignik, Alaska",earthquake,,3.9,,,reviewed,ak,ak
2022-01-20T11:26:00.970Z,35.7196667,-117.565,8.94,0.67,ml,15,148,0.09945,0.1,ci,ci39918015,2022-01-20T16:41:57.829Z,"15km NE of Ridgecrest, CA",earthquake,0.2,0.54,0.121,3,reviewed,ci,ci
2022-01-20T11:21:05.560Z,35.9758333,-117.3838333,2.35,1.48,ml,18,165,0.1176,0.14,ci,ci39918007,2022-01-20T13:36:44.228Z,"23km N of Searles Valley, CA",earthquake,0.39,0.99,0.104,17,reviewed,ci,ci
2022-01-20T11:20:59.980Z,19.2211666107178,-155.427337646484,34.4599990844727,2.29,ml,50,130,,0.129999995,hv,hv72882702,2022-01-21T09:18:37.040Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.54,0.699999988,2.75,11,automatic,hv,hv
2022-01-20T11:09:06.870Z,19.1401672363281,-155.483993530273,30.6200008392334,1.97000003,md,36,168,,0.180000007,hv,hv72882692,2022-01-20T11:12:15.730Z,"6 km S of Pāhala, Hawaii",earthquake,0.74,1.19000006,0.980000019,3,automatic,hv,hv
2022-01-20T11:00:45.060Z,38.8338318,-122.8171692,1.52,0.85,md,10,75,0.0118,0.02,nc,nc73680991,2022-01-20T11:02:23.874Z,"8km NW of The Geysers, CA",earthquake,0.38,0.72,,1,automatic,nc,nc
2022-01-20T10:58:10.086Z,-14.9692,167.9209,10,5.4,mww,,46,0.84,1.44,us,us7000gdi9,2022-01-21T11:01:43.684Z,"91 km E of Port-Olry, Vanuatu",earthquake,6.4,1.7,0.08,15,reviewed,us,us
2022-01-20T10:46:06.920Z,35.523,-117.4076667,8.99,1.81,ml,25,71,0.03524,0.15,ci,ci39917999,2022-01-20T13:37:37.940Z,"26km NE of Johannesburg, CA",earthquake,0.26,0.47,0.16,26,reviewed,ci,ci
2022-01-20T10:44:47.530Z,37.5025,-121.4096667,7.15,0.88,md,10,114,0.06515,0.04,nc,nc73680986,2022-01-20T17:56:27.568Z,"19km WSW of Westley, CA",earthquake,0.6,0.91,0.363,10,reviewed,nc,nc
2022-01-20T10:44:17.745Z,-2.4778,140.0024,27.2,5.4,mww,,25,7.37,0.98,us,us7000gdi6,2022-01-21T10:48:29.177Z,"71 km W of Abepura, Indonesia",earthquake,8.4,3.8,0.093,11,reviewed,us,us
2022-01-20T10:43:56.428Z,-21.6898,-67.4847,214.21,4.2,mb,,73,1.411,0.96,us,us7000gdi3,2022-01-21T09:05:35.040Z,"152 km SSW of Uyuni, Bolivia",earthquake,10.1,13.7,0.372,2,reviewed,us,us
2022-01-20T10:38:33.690Z,19.2229995727539,-155.432662963867,33.060001373291,1.75,md,42,126,,0.100000001,hv,hv72882657,2022-01-20T10:41:41.720Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.51,0.649999976,1.75,4,automatic,hv,hv
2022-01-20T10:35:19.010Z,33.7305,-116.8961667,4.95,1.53,ml,70,31,0.09061,0.21,ci,ci39917991,2022-01-20T19:09:38.670Z,"2km S of Valle Vista, CA",earthquake,0.13,0.4,0.284,24,reviewed,ci,ci
2022-01-20T10:35:11.762Z,31.56272287,-104.1242555,6.080151367,2.2,ml,24,54,0.06609255661,0.2,tx,tx2022bjnn,2022-01-22T00:01:49.439Z,"41 km NW of Toyah, Texas",earthquake,0.7110049856,0.8965917415,0.2,12,reviewed,tx,tx
2022-01-20T10:32:06.230Z,33.3803333,-116.871,6.38,0.52,ml,36,30,0.02755,0.19,ci,ci39917983,2022-01-20T19:20:20.986Z,"3km NNW of Palomar Observatory, CA",earthquake,0.19,0.44,0.073,14,reviewed,ci,ci
2022-01-20T10:26:21.929Z,36.11366667,-97.86783333,6.88,2.04,ml,93,35,0,0.18,ok,ok2022bjnf,2022-01-20T13:27:36.631Z,"2 km E of Hennessey, Oklahoma",earthquake,,0.4,0.3,39,reviewed,ok,ok
2022-01-20T10:26:15.737Z,64.5261,-147.1194,4,1.8,ml,,,,0.49,ak,ak022x8uvr5,2022-01-20T10:38:35.700Z,"10 km W of Salcha, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-20T10:19:40.430Z,38.7905006,-122.7613297,2.07,0.86,md,14,62,0.01019,0.02,nc,nc73680976,2022-01-20T10:21:18.244Z,"2km NNW of The Geysers, CA",earthquake,0.33,0.61,0.01,3,automatic,nc,nc
2022-01-20T10:12:03.850Z,19.2140007019043,-155.426498413086,33.4099998474121,1.94000006,md,32,150,,0.0900000036,hv,hv72882632,2022-01-20T10:15:18.160Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.61,0.779999971,1.94000006,4,automatic,hv,hv
2022-01-20T10:11:39.887Z,61.8985,-153.8795,0,1.8,ml,,,,0.98,ak,ak022x8rqj1,2022-01-20T10:28:44.257Z,"102 km NE of Lime Village, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-20T10:07:05.890Z,33.8148333,-117.708,7.11,0.7,ml,24,78,0.05384,0.15,ci,ci39917975,2022-01-20T18:55:11.661Z,"10km E of Villa Park, CA",earthquake,0.23,0.56,0.069,5,reviewed,ci,ci
2022-01-20T10:00:12.501Z,44.3507,-115.217,10,2.5,ml,,56,0.845,0.91,us,us7000gdhr,2022-01-21T08:54:34.837Z,"southern Idaho",earthquake,1.9,2,0.059,38,reviewed,us,us
2022-01-20T09:52:39.430Z,59.9781666666667,-153.071833333333,-2.67,-0.15,ml,4,143,,0.08,av,av91468071,2022-01-21T17:47:54.660Z,"61 km ENE of Pedro Bay, Alaska",earthquake,0.29,1.37,0.226988737959889,4,reviewed,av,av
2022-01-20T09:52:30.400Z,35.5243333,-117.4053333,8.7,2.53,ml,37,47,0.03329,0.13,ci,ci39917967,2022-01-21T08:47:27.040Z,"27km ESE of Ridgecrest, CA",earthquake,0.16,0.3,0.178,96,reviewed,ci,ci
2022-01-20T09:46:19.743Z,60.0788,-152.2497,78.3,1.9,ml,,,,0.55,ak,ak022x8dqs5,2022-01-20T09:51:50.118Z,"32 km WNW of Happy Valley, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T09:43:19.720Z,33.5915,-116.8048333,6.46,0.35,ml,17,75,0.03407,0.09,ci,ci39917959,2022-01-20T19:09:30.108Z,"13km WNW of Anza, CA",earthquake,0.23,0.44,0.075,4,reviewed,ci,ci
2022-01-20T09:38:12.740Z,61.413,-152.234,0,1.5,ml,,,,1.09,ak,ak022x8c0ip,2022-01-21T17:44:37.720Z,"68 km WNW of Beluga, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T09:32:36.570Z,38.8253326,-122.802002,3.82,0.35,md,8,78,0.01592,0.03,nc,nc73680956,2022-01-20T09:34:14.640Z,"7km NW of The Geysers, CA",earthquake,0.7,2.72,,1,automatic,nc,nc
2022-01-20T09:29:56.440Z,19.2058334350586,-155.422164916992,32.8699989318848,2.37,ml,50,153,,0.109999999,hv,hv72882572,2022-01-20T09:35:27.910Z,"5 km E of Pāhala, Hawaii",earthquake,0.49,0.600000024,4.03,5,automatic,hv,hv
2022-01-20T09:29:12.460Z,59.9965,-152.8861,110,1.4,ml,,,,0.42,ak,ak022x8a31q,2022-01-20T09:32:47.568Z,"63 km WNW of Anchor Point, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-20T09:24:06.963Z,38.167,-117.8757,13.2,0.8,ml,9,163.88,0.072,0.3336,nn,nn00832025,2022-01-20T09:28:11.277Z,"32 km SE of Mina, Nevada",earthquake,,0.9,0.49,4,automatic,nn,nn
2022-01-20T09:21:59.700Z,19.1651668548584,-155.469497680664,32.3400001525879,1.70000005,md,37,162,,0.159999996,hv,hv72882567,2022-01-20T09:25:12.370Z,"Island of Hawaii, Hawaii",earthquake,0.53,0.99000001,0.850000024,3,automatic,hv,hv
2022-01-20T09:19:50.310Z,19.4108333587646,-155.266006469727,1,1.75999999,md,13,59,,0.349999994,hv,hv72882552,2022-01-20T09:22:45.520Z,"4 km SW of Volcano, Hawaii",earthquake,0.48,0.469999999,1.16999996,8,automatic,hv,hv
2022-01-20T09:14:21.258Z,36.7006,-116.2932,4.3,0,ml,6,257.18,0.07,0.0866,nn,nn00832108,2022-01-21T02:37:41.380Z,"47 km ESE of Beatty, Nevada",earthquake,,5.7,0.38,4,reviewed,nn,nn
2022-01-20T08:55:23.272Z,36.7486,-115.9002,0.9,0.2,ml,4,288.32,0.061,0.1763,nn,nn00832107,2022-01-21T02:37:40.572Z,"28 km NW of Indian Springs, Nevada",earthquake,,20.7,0,1,reviewed,nn,nn
2022-01-20T08:50:55.720Z,51.6431,-175.6091,36.31,4.1,mb,,183,0.53,0.78,us,us7000gdhd,2022-01-20T17:59:53.871Z,"75 km ESE of Adak, Alaska",earthquake,6.7,11.4,0.066,63,reviewed,us,us
2022-01-20T08:47:31.880Z,33.3351667,-116.3805,9.21,0.73,ml,17,78,0.014,0.14,ci,ci39917951,2022-01-20T19:06:58.907Z,"9km N of Borrego Springs, CA",earthquake,0.26,0.57,0.201,10,reviewed,ci,ci
2022-01-20T08:43:33.015Z,51.9594,178.981,119.4,2.7,ml,,,,0.53,ak,ak022x7rpon,2022-01-20T17:54:18.445Z,"Rat Islands, Aleutian Islands, Alaska",earthquake,,0.5,,,reviewed,ak,ak
2022-01-20T08:40:13.040Z,33.3346667,-116.2038333,11.34,0.91,ml,31,79,0.09274,0.18,ci,ci39917943,2022-01-20T19:03:52.870Z,"18km SW of Oasis, CA",earthquake,0.3,0.48,0.068,15,reviewed,ci,ci
2022-01-20T08:29:43.678Z,-20.8171,-175.5203,10,4.6,mb,,124,6.795,0.56,us,us7000gdqc,2022-01-21T02:02:04.040Z,"48 km NW of Nuku‘alofa, Tonga",earthquake,6.9,1.9,0.122,20,reviewed,us,us
2022-01-20T08:10:16.030Z,38.7869987,-122.7683334,1.49,0.59,md,12,103,0.02794,0.03,nc,nc73680936,2022-01-20T08:11:53.048Z,"2km NW of The Geysers, CA",earthquake,0.28,0.88,0.04,2,automatic,nc,nc
2022-01-20T08:10:04.530Z,34.2983333,-118.3925,9.3,0.81,ml,17,155,0.0142,0.12,ci,ci39917927,2022-01-20T18:58:46.557Z,"4km NW of Lake View Terrace, CA",earthquake,0.29,0.51,0.153,10,reviewed,ci,ci
2022-01-20T08:04:33.190Z,46.1155,-122.336,17.08,0.18,ml,6,274,0.05354,0.07,uw,uw61802957,2022-01-20T19:42:04.170Z,"24 km NNE of Amboy, Washington",earthquake,0.64,0.73,0.126668396488982,4,reviewed,uw,uw
2022-01-20T08:02:38.033Z,61.1665,-151.9527,71.3,1.3,ml,,,,0.81,ak,ak022x7ix41,2022-01-20T08:06:28.442Z,"45 km WNW of Tyonek, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-20T08:01:28.450Z,46.1156666666667,-122.336666666667,17.07,0.55,ml,5,273,0.05339,0.06,uw,uw61802952,2022-01-20T19:49:05.810Z,"Washington",earthquake,0.7,0.61,0.128183138695749,4,reviewed,uw,uw
2022-01-20T07:59:55.800Z,46.0913333333333,-122.386666666667,14.92,1.18,ml,25,64,0.08599,0.22,uw,uw61802947,2022-01-20T18:40:05.190Z,"20 km NNE of Amboy, Washington",earthquake,0.42,0.89,0.0967287351761605,10,reviewed,uw,uw
2022-01-20T07:57:17.450Z,19.174165725708,-155.484664916992,35.0699996948242,1.95000005,md,36,91,,0.100000001,hv,hv72882507,2022-01-20T08:00:34.550Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.57,0.850000024,1.95000005,4,automatic,hv,hv
2022-01-20T07:56:02.864Z,59.7985,-152.592,81,1.5,ml,,,,0.44,ak,ak022x78zfm,2022-01-20T08:00:07.475Z,"42 km W of Anchor Point, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T07:55:25.650Z,38.8193321,-122.8083344,3.05,1.17,md,18,54,0.004279,0.02,nc,nc73680926,2022-01-20T08:27:11.883Z,"6km NW of The Geysers, CA",earthquake,0.28,0.72,,1,automatic,nc,nc
2022-01-20T07:54:07.960Z,19.2468338012695,-155.432159423828,34.6199989318848,1.98000002,md,43,116,,0.129999995,hv,hv72882502,2022-01-20T07:57:16.470Z,"6 km NE of Pāhala, Hawaii",earthquake,0.62,0.870000005,0.980000019,8,automatic,hv,hv
2022-01-20T07:45:12.880Z,33.7313333,-116.8951667,2.69,0.99,ml,33,83,0.09162,0.19,ci,ci39917903,2022-01-20T13:38:29.239Z,"2km S of Valle Vista, CA",earthquake,0.24,0.51,0.196,25,reviewed,ci,ci
2022-01-20T07:44:09.007Z,-57.2654,-25.2069,35,4.9,mb,,95,7.029,0.55,us,us7000gdh2,2022-01-20T08:06:02.040Z,"South Sandwich Islands region",earthquake,12.7,2,0.067,71,reviewed,us,us
2022-01-20T07:43:09.920Z,33.1648333,-116.4178333,10.31,0.91,ml,35,54,0.08895,0.17,ci,ci39917895,2022-01-20T18:54:25.290Z,"11km SSW of Borrego Springs, CA",earthquake,0.22,0.49,0.192,19,reviewed,ci,ci
2022-01-20T07:42:07.869Z,59.9062,-140.1592,19.8,2.3,ml,,,,1.36,ak,ak022x75zsi,2022-01-20T07:46:15.826Z,"46 km NNW of Yakutat, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-20T07:34:14.506Z,36.8581,-117.3877,4.7,0.9,ml,10,222.9,0.139,0.3176,nn,nn00832023,2022-01-20T07:38:30.686Z,"56 km W of Beatty, Nevada",earthquake,,1.1,0.79,5,automatic,nn,nn
2022-01-20T07:31:24.590Z,60.0541,-153.23,126,1.6,ml,,,,0.5,ak,ak022x73o3t,2022-01-20T07:36:34.633Z,"57 km ENE of Pedro Bay, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T07:28:09.810Z,32.7738333,-115.4408333,11.81,1.7,ml,30,81,0.0318,0.24,ci,ci39917887,2022-01-20T18:20:09.298Z,"7km SW of Holtville, CA",earthquake,0.39,0.45,0.149,19,reviewed,ci,ci
2022-01-20T07:00:15.700Z,19.2428340911865,-155.4306640625,31.3199996948242,1.82000005,md,45,118,,0.140000001,hv,hv72882432,2022-01-20T07:03:34.360Z,"6 km NE of Pāhala, Hawaii",earthquake,0.47,0.779999971,0.930000007,16,automatic,hv,hv
2022-01-20T06:54:00.840Z,38.8600006,-122.7985001,2.48,0.87,md,9,163,0.005243,0.01,nc,nc73680911,2022-01-20T06:55:37.508Z,"8km WNW of Cobb, CA",earthquake,0.54,1.25,,1,automatic,nc,nc
2022-01-20T06:52:34.130Z,37.6626667,-118.8925,2.98,-0.18,md,11,143,0.01309,0.02,nc,nc73680916,2022-01-20T16:47:51.196Z,"8km ENE of Mammoth Lakes, CA",earthquake,0.67,0.95,0.249,11,reviewed,nc,nc
2022-01-20T06:52:21.240Z,38.8373337,-122.8205032,1.67,0.86,md,8,137,0.01177,0.03,nc,nc73680906,2022-01-20T06:53:58.356Z,"9km WNW of Cobb, CA",earthquake,0.48,0.88,,1,automatic,nc,nc
2022-01-20T06:52:21.129Z,-58.9,-23.9049,10,5.6,mww,,48,8.338,0.83,us,us7000gdfw,2022-01-21T06:56:25.824Z,"South Sandwich Islands region",earthquake,9.5,1.9,0.098,10,reviewed,us,us
2022-01-20T06:40:38.996Z,63.0886,-151.5264,0,1.7,ml,,,,0.54,ak,ak022x6k76u,2022-01-20T07:21:12.689Z,"51 km S of Denali National Park, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-20T06:37:16.491Z,39.4159,-119.9423,7.6,1.2,ml,28,37.1,0.094,0.1368,nn,nn00832019,2022-01-21T02:36:58.396Z,"7 km ENE of Floriston, California",earthquake,,1.2,0.21,11,reviewed,nn,nn
2022-01-20T06:35:45.466Z,36.6646,-115.9998,0,-0.2,ml,6,269.22,0.065,0.1106,nn,nn00832104,2022-01-21T02:37:39.851Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.2,2,reviewed,nn,nn
2022-01-20T06:34:56.570Z,38.8441658,-122.8251648,1.76,0.37,md,8,130,0.009797,0.01,nc,nc73680901,2022-01-20T06:36:30.958Z,"9km WNW of Cobb, CA",earthquake,0.64,0.9,,1,automatic,nc,nc
2022-01-20T06:33:54.659Z,38.1936,-117.806,3.4,1.6,ml,15,119.32,0.132,0.1836,nn,nn00832017,2022-01-20T06:49:59.526Z,"34 km SE of Mina, Nevada",earthquake,,1.2,0.18,9,automatic,nn,nn
2022-01-20T06:33:38.450Z,35.6628333,-117.4325,6.84,-0.13,ml,5,177,0.07992,0.04,ci,ci39917871,2022-01-20T16:37:56.735Z,"12km SSW of Searles Valley, CA",earthquake,1.38,1.19,0.063,1,reviewed,ci,ci
2022-01-20T06:32:25.795Z,-10.2085,-75.4936,21.35,4.6,mb,,149,3.695,0.53,us,us7000gdg0,2022-01-21T19:00:38.744Z,"42 km NNW of Oxapampa, Peru",earthquake,8.7,6.2,0.056,95,reviewed,us,us
2022-01-20T06:30:04.850Z,39.4185,-110.3003333,-3.29,2.03,md,8,199,0.01998,0.12,uu,uu60478237,2022-01-20T16:34:47.920Z,"16 km SSE of Sunnyside, Utah",earthquake,0.84,2.79,0.122,7,reviewed,uu,uu
2022-01-20T06:27:36.728Z,36.6608,-115.9958,0,-0.5,ml,6,275.11,0.068,0.1039,nn,nn00832103,2022-01-21T02:37:38.939Z,"30 km WNW of Indian Springs, Nevada",earthquake,,0,0,1,reviewed,nn,nn
2022-01-20T06:26:19.520Z,19.392333984375,-155.254669189453,2.69000005722046,1.79,ml,13,61,,0.219999999,hv,hv72882402,2022-01-20T06:31:50.150Z,"5 km SSW of Volcano, Hawaii",earthquake,0.42,0.319999993,0.34,7,automatic,hv,hv
2022-01-20T06:25:59.190Z,39.4176667,-110.2975,-3.22,1.72,ml,8,200,0.02232,0.15,uu,uu60478232,2022-01-20T16:32:38.330Z,"16 km SSE of Sunnyside, Utah",earthquake,0.97,2.7,0.11,3,reviewed,uu,uu
2022-01-20T06:23:42.710Z,38.8474998,-122.8166656,1.37,0.86,md,13,57,0.008852,0.03,nc,nc73680896,2022-01-20T06:25:16.394Z,"9km WNW of Cobb, CA",earthquake,0.26,0.52,,1,automatic,nc,nc
2022-01-20T06:19:25.850Z,33.323,-116.8751667,9.96,0.72,ml,35,34,0.03228,0.16,ci,ci39917863,2022-01-20T18:15:15.895Z,"4km SSW of Palomar Observatory, CA",earthquake,0.19,0.45,0.195,18,reviewed,ci,ci
2022-01-20T06:14:15.090Z,37.8665,-118.6056667,0.45,1.18,md,12,327,0.2504,0.08,nc,nc73680891,2022-01-20T17:08:10.806Z,"34km N of Toms Place, CA",earthquake,2.42,4.01,0.158,13,reviewed,nc,nc
2022-01-20T06:08:24.003Z,60.629,-152.1381,74.8,1.4,ml,,,,0.56,ak,ak022x6db35,2022-01-20T06:11:35.068Z,"44 km W of Salamatof, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-20T06:00:48.530Z,34.4401667,-117.737,7.21,0.98,ml,17,136,0.07566,0.14,ci,ci39917855,2022-01-20T18:08:56.367Z,"8km SE of Llano, CA",earthquake,0.3,0.64,0.082,17,reviewed,ci,ci
2022-01-20T05:57:37.624Z,38.1166,-118.0656,2,0.4,ml,8,198.93,0.086,0.2504,nn,nn00832013,2022-01-20T06:01:29.709Z,"30 km S of Mina, Nevada",earthquake,,5.7,0.2,3,automatic,nn,nn
2022-01-20T05:56:26.470Z,36.0673333,-118.0033333,4.65,0.51,ml,19,51,0.05668,0.14,ci,ci39917847,2022-01-20T17:57:39.207Z,"6km WNW of Coso Junction, CA",earthquake,0.28,0.61,0.267,6,reviewed,ci,ci
2022-01-20T05:55:20.987Z,36.5611,70.9655,205.1,4.5,mb,,58,0.644,0.67,us,us7000gdfj,2022-01-20T07:21:40.040Z,"35 km SSE of Jurm, Afghanistan",earthquake,5.1,5,0.062,75,reviewed,us,us
2022-01-20T05:54:42.643Z,-18.0352,-177.9422,627.76,4.4,mb,,177,3.71,0.44,us,us7000gdfk,2022-01-20T06:41:29.040Z,"290 km E of Levuka, Fiji",earthquake,14.9,11.3,0.086,39,reviewed,us,us
2022-01-20T05:43:19.739Z,61.2269,-142.6961,29.9,2.4,ml,,,,0.52,ak,ak022x5zd7v,2022-01-20T05:50:12.347Z,"25 km SSE of McCarthy, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-20T05:41:32.011Z,31.67205249,-104.4907005,6.620019531,2.4,ml,39,74,0.009255009912,0.3,tx,tx2022bjdv,2022-01-20T22:56:03.960Z,"56 km S of Whites City, New Mexico",earthquake,1.429642939,1.155765309,0.2,19,reviewed,tx,tx
2022-01-20T05:37:34.480Z,33.8771667,-119.5905,5.8,1.9,ml,22,155,0.4185,0.24,ci,ci39917831,2022-01-20T18:04:36.344Z,"18km SSW of Santa Cruz Is. (E end), CA",earthquake,0.56,31.61,0.162,28,reviewed,ci,ci
2022-01-20T05:35:26.575Z,51.5151,-176.1969,35,3.9,mb,,204,0.37,0.97,us,us7000gdfi,2022-01-20T06:31:26.040Z,"50 km SE of Adak, Alaska",earthquake,3.6,2,0.112,21,reviewed,us,us
2022-01-20T05:24:50.100Z,46.856,-121.756166666667,1.81,0.04,ml,10,88,0.02577,0.06,uw,uw61802932,2022-01-20T19:55:32.500Z,"23 km ENE of Ashford, Washington",earthquake,0.26,0.65,0.164652308811103,4,reviewed,uw,uw
2022-01-20T05:24:03.180Z,39.4201667,-110.3035,-2.18,2.09,md,7,198,0.01719,0.12,uu,uu60478227,2022-01-20T16:33:12.110Z,"16 km SSE of Sunnyside, Utah",earthquake,1.12,1.4,0.21,5,reviewed,uu,uu
2022-01-20T05:14:34.430Z,19.2298336029053,-155.410659790039,31.1900005340576,2.24,ml,42,136,,0.170000002,hv,hv72882327,2022-01-20T08:18:29.040Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.57,0.75,2.61,12,automatic,hv,hv
2022-01-20T05:11:52.300Z,38.8246651,-122.8535004,2,1.18,md,19,63,0.0039,0.02,nc,nc73680886,2022-01-20T05:44:11.188Z,"10km WNW of The Geysers, CA",earthquake,0.21,0.4,0.01,3,automatic,nc,nc
2022-01-20T05:06:00.487Z,-31.8944,57.5642,10,5,mb,,110,10.803,0.78,us,us7000gdfb,2022-01-20T05:23:38.040Z,"Southwest Indian Ridge",earthquake,13.5,1.9,0.124,21,reviewed,us,us
2022-01-20T05:05:42.260Z,38.7886667,-122.7648333,2.15,0.43,md,20,81,0.01259,0.03,nc,nc73680881,2022-01-22T22:25:32.882Z,"2km NNW of The Geysers, CA",earthquake,0.25,0.39,0.134,3,reviewed,nc,nc
2022-01-20T05:01:38.648Z,36.6652,-115.9986,0,-0.3,ml,7,269.64,0.064,0.1012,nn,nn00832101,2022-01-21T02:37:38.049Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.36,3,reviewed,nn,nn
2022-01-20T04:59:35.845Z,36.6744,-116.0036,3.4,1,ml,24,121.53,0.056,0.1378,nn,nn00832012,2022-01-21T02:36:43.438Z,"31 km WNW of Indian Springs, Nevada",earthquake,,2.2,0.51,15,reviewed,nn,nn
2022-01-20T04:58:25.810Z,37.4888333,-118.8543333,0.3,0.42,md,8,328,0.103,0.06,nc,nc73680876,2022-01-20T16:23:19.017Z,"17km WSW of Toms Place, CA",earthquake,2.47,31.61,0.278,7,reviewed,nc,nc
2022-01-20T04:49:57.747Z,61.1933,-149.2581,25.6,1.9,ml,,,,0.85,ak,ak022x5fauo,2022-01-20T04:54:05.812Z,"21 km ESE of Elmendorf Air Force Base, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-20T04:47:21.969Z,38.1591,-117.7894,14.2,0.9,ml,8,157.54,0.104,0.1401,nn,nn00832011,2022-01-20T04:51:29.803Z,"37 km SE of Mina, Nevada",earthquake,,2.2,0.27,4,automatic,nn,nn
2022-01-20T04:42:36.332Z,36.6668,-115.9999,0,-0.2,ml,10,246.53,0.063,0.1226,nn,nn00832100,2022-01-21T02:37:37.108Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.15,5,reviewed,nn,nn
2022-01-20T04:39:14.840Z,33.7345,-116.8945,6.13,0.83,ml,34,72,0.093,0.14,ci,ci39917823,2022-01-20T17:53:51.018Z,"2km S of Valle Vista, CA",earthquake,0.2,0.54,0.206,19,reviewed,ci,ci
2022-01-20T04:37:25.750Z,33.6446667,-116.7255,13.6,0.46,ml,13,82,0.04944,0.05,ci,ci39917815,2022-01-20T15:48:12.863Z,"11km S of Idyllwild, CA",earthquake,0.23,0.36,0.082,2,reviewed,ci,ci
2022-01-20T04:37:03.820Z,19.2189998626709,-155.431503295898,32.5900001525879,2.32,ml,46,129,,0.119999997,hv,hv72882282,2022-01-20T04:42:33.810Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.47,0.720000029,4.47,7,automatic,hv,hv
2022-01-20T04:34:55.990Z,38.8266678,-122.7978363,2.84,0.84,md,8,114,0.0101,0.02,nc,nc73680866,2022-01-20T04:36:31.840Z,"6km W of Cobb, CA",earthquake,0.51,0.95,,1,automatic,nc,nc
2022-01-20T04:32:35.819Z,60.5412,-152.1907,83.7,1.6,ml,,,,0.33,ak,ak022x5blyu,2022-01-20T04:37:13.790Z,"48 km W of Salamatof, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-20T04:32:17.377Z,31.19653858,-103.3310081,5.771655273,2.7,ml,36,42,0.05364811156,0.3,tx,tx2022bjbn,2022-01-21T06:21:36.040Z,"25 km WSW of Coyanosa, Texas",earthquake,0.8893542923,0.7993849657999998,0.1,14,reviewed,tx,tx
2022-01-20T04:31:07.530Z,38.7658348,-122.7283325,0.71,1.17,md,12,78,0.00503,0.05,nc,nc73680861,2022-01-20T05:14:11.011Z,"3km ESE of The Geysers, CA",earthquake,0.28,0.34,0.04,4,automatic,nc,nc
2022-01-20T04:30:18.260Z,19.2194995880127,-155.421661376953,33.0499992370605,2.19000006,md,43,135,,0.129999995,hv,hv72882272,2022-01-20T04:33:34.060Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.61,0.709999979,1.04999995,19,automatic,hv,hv
2022-01-20T04:26:10.480Z,33.7298333,-116.8985,3.9,2.97,ml,123,13,0.08856,0.19,ci,ci39917799,2022-01-21T05:58:38.040Z,"2km SSW of Valle Vista, CA",earthquake,0.1,0.35,0.128,185,reviewed,ci,ci
2022-01-20T04:25:59.100Z,33.7363333,-116.896,2.82,0.65,ml,25,101,0.09234,0.16,ci,ci39917791,2022-01-20T18:26:50.624Z,"1km S of Valle Vista, CA",earthquake,0.23,0.87,0.148,14,reviewed,ci,ci
2022-01-20T04:25:35.660Z,33.7336667,-116.8955,4.19,0.78,ml,29,49,0.09197,0.13,ci,ci39917783,2022-01-20T18:17:50.976Z,"2km S of Valle Vista, CA",earthquake,0.19,0.42,0.151,13,reviewed,ci,ci
2022-01-20T04:23:11.835Z,64.7096,-145.6446,10.6,1.8,ml,,,,0.76,ak,ak022x59mof,2022-01-20T04:27:22.501Z,"59 km NE of Harding-Birch Lakes, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-20T04:16:42.526Z,36.6704,-116.0029,0,-0.3,ml,7,263.71,0.06,0.0733,nn,nn00832099,2022-01-21T02:37:36.141Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.21,3,reviewed,nn,nn
2022-01-20T04:16:24.050Z,34.4396667,-117.7351667,7.61,0.85,ml,15,137,0.07431,0.12,ci,ci39917775,2022-01-20T18:06:10.348Z,"8km SE of Llano, CA",earthquake,0.25,0.54,0.192,9,reviewed,ci,ci
2022-01-20T04:14:51.333Z,31.18459582,-103.3347856,4.948999022999999,2.3,ml,24,39,0.05608259166,0.3,tx,tx2022bjaz,2022-01-20T23:31:45.570Z,"26 km WSW of Coyanosa, Texas",earthquake,1.100154406,0.9408666893,0.1,10,reviewed,tx,tx
2022-01-20T04:14:00.220Z,34.4391667,-117.7348333,6.9,0.91,ml,21,114,0.07375,0.14,ci,ci39917767,2022-01-20T17:50:16.827Z,"8km SE of Llano, CA",earthquake,0.26,0.59,0.185,12,reviewed,ci,ci
2022-01-20T04:12:46.563Z,36.6661,-115.9974,0,-0.1,ml,8,260.55,0.063,0.098,nn,nn00832095,2022-01-21T02:37:31.557Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.22,4,reviewed,nn,nn
2022-01-20T04:09:13.450Z,33.195,-116.3901667,11.48,2.05,ml,86,21,0.07643,0.19,ci,ci39917759,2022-01-20T17:43:35.680Z,"7km SSW of Borrego Springs, CA",earthquake,0.13,0.27,0.155,61,reviewed,ci,ci
2022-01-20T04:07:14.418Z,61.0407,-152.2896,110.4,2.2,ml,,,,0.57,ak,ak022x567ii,2022-01-20T04:11:10.708Z,"62 km W of Tyonek, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-20T04:01:57.240Z,39.418,-110.3035,-2.29,1.85,md,6,198,0.01781,0.12,uu,uu60478222,2022-01-20T16:29:00.230Z,"16 km SSE of Sunnyside, Utah",earthquake,1.06,2.53,0.21,6,reviewed,uu,uu
2022-01-20T03:59:32.470Z,34.1915,-116.949,10.08,1.27,ml,41,56,0.0744,0.14,ci,ci39917735,2022-01-20T14:48:07.384Z,"7km SSW of Big Bear Lake, CA",earthquake,0.19,0.36,0.112,32,reviewed,ci,ci
2022-01-20T03:57:18.970Z,39.4205,-110.3038333,-2.26,2.01,md,7,197,0.01686,0.12,uu,uu60478217,2022-01-20T16:27:56.100Z,"16 km SSE of Sunnyside, Utah",earthquake,0.98,2.35,0.109,6,reviewed,uu,uu
2022-01-20T03:50:34.720Z,17.8935,-65.6743,4,3.12,md,15,232,0.2373,0.4,pr,pr2022020001,2022-01-22T02:05:28.862Z,"24 km SE of El Negro, Puerto Rico",earthquake,1.21,0.71,0.08,6,reviewed,pr,pr
2022-01-20T03:50:34.070Z,35.8921667,-117.6618333,9.61,-0.17,ml,5,100,0.05639,0.16,ci,ci39917711,2022-01-20T16:27:59.757Z,"23km ESE of Little Lake, CA",earthquake,0.69,1.54,0.107,2,reviewed,ci,ci
2022-01-20T03:41:45.004Z,31.18278101,-103.348713,3.45793457,3.1,ml,27,40,0.06809757395,0.3,tx,tx2022bizw,2022-01-21T05:49:03.040Z,"27 km SE of Lindsay, Texas",earthquake,0.7648003196,1.639951598,0.1,14,reviewed,tx,tx
2022-01-20T03:30:38.749Z,-37.3631,-74.2413,10,3.8,ml,,155,1.041,0.49,us,us7000gdeh,2022-01-21T05:34:38.040Z,"58 km WNW of Lebu, Chile",earthquake,3.1,1.9,,,reviewed,us,guc
2022-01-20T03:24:08.710Z,19.220666885376,-155.471160888672,33.3300018310547,1.76999998,md,27,184,,0.150000006,hv,hv72882237,2022-01-20T03:27:15.440Z,"2 km NNE of Pāhala, Hawaii",earthquake,0.79,1.02999997,1.00999999,3,automatic,hv,hv
2022-01-20T03:17:02.664Z,36.6803,-116.005,0,-0.3,ml,8,250.57,0.051,0.074,nn,nn00832094,2022-01-21T02:37:30.579Z,"32 km WNW of Indian Springs, Nevada",earthquake,,0,0.12,3,reviewed,nn,nn
2022-01-20T03:16:45.949Z,36.6674,-115.9966,0,-0.2,ml,8,269.88,0.062,0.1152,nn,nn00832093,2022-01-21T02:37:29.664Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.14,4,reviewed,nn,nn
2022-01-20T03:11:10.742Z,36.664,-116.0018,0,0.3,ml,9,260.5,0.066,0.0942,nn,nn00832092,2022-01-21T02:37:28.694Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.43,5,reviewed,nn,nn
2022-01-20T03:08:19.930Z,33.5871667,-116.8071667,6.52,0.54,ml,28,39,0.03653,0.11,ci,ci39917687,2022-01-20T17:25:47.100Z,"13km WNW of Anza, CA",earthquake,0.14,0.29,0.084,10,reviewed,ci,ci
2022-01-20T03:06:12.570Z,-20.7028,-175.3846,10,4.6,mb,,129,6.862,0.6,us,us7000gdqg,2022-01-21T02:16:56.040Z,"51 km NNW of Nuku‘alofa, Tonga",earthquake,15.9,1.9,0.182,9,reviewed,us,us
2022-01-20T02:50:37.920Z,33.2891667,-116.739,14.15,0.68,ml,40,45,0.05557,0.14,ci,ci39917671,2022-01-20T17:19:47.264Z,"6km NNE of Lake Henshaw, CA",earthquake,0.17,0.33,0.128,16,reviewed,ci,ci
2022-01-20T02:41:55.084Z,36.676,-116.0032,3.5,1,ml,26,121.25,0.055,0.1304,nn,nn00832007,2022-01-21T02:36:42.251Z,"32 km WNW of Indian Springs, Nevada",earthquake,,1.5,0.95,16,reviewed,nn,nn
2022-01-20T02:40:21.540Z,19.201000213623,-155.476669311523,32.8199996948242,2.18,ml,45,88,,0.100000001,hv,hv72882182,2022-01-20T02:45:52.370Z,"0 km SE of Pāhala, Hawaii",earthquake,0.52,0.860000014,5.22,3,automatic,hv,hv
2022-01-20T02:38:39.661Z,61.4575,-149.879,31.1,1.8,ml,,,,0.59,ak,ak022x461cl,2022-01-20T02:49:42.150Z,"8 km W of Knik, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-20T02:34:41.960Z,38.833168,-122.8143311,0.97,0.85,md,11,53,0.01031,0.01,nc,nc73680836,2022-01-20T02:36:20.832Z,"8km NW of The Geysers, CA",earthquake,0.29,1.05,,1,automatic,nc,nc
2022-01-20T02:32:36.271Z,11.2845,-86.923,35,4.9,mb,,161,1.083,0.55,us,us7000gdeb,2022-01-21T05:17:00.040Z,"71 km SW of Masachapa, Nicaragua",earthquake,5.6,2,0.031,331,reviewed,us,us
2022-01-20T02:30:43.200Z,48.6248333333333,-123.059166666667,14.37,1.53,ml,21,91,0.04635,0.2,uw,uw61802922,2022-01-20T18:57:54.120Z,"8 km WNW of Orcas, Washington",earthquake,0.37,0.69,0.160956611561544,7,reviewed,uw,uw
2022-01-20T02:23:57.264Z,36.6556,-115.9877,0,-0.3,ml,7,280.65,0.073,0.1722,nn,nn00832091,2022-01-21T02:37:27.733Z,"29 km WNW of Indian Springs, Nevada",earthquake,,0,0.1,4,reviewed,nn,nn
2022-01-20T02:09:33.270Z,39.4175,-110.2938333,-3.36,1.86,md,6,201,0.0251,0.11,uu,uu60478212,2022-01-20T16:25:50.340Z,"16 km SSE of Sunnyside, Utah",earthquake,1.39,3.3,0.242,6,reviewed,uu,uu
2022-01-20T02:06:25.347Z,65.0201,-147.0323,5,1.4,ml,,,,0.95,ak,ak022x3z5c6,2022-01-20T02:22:28.772Z,"16 km N of Two Rivers, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-20T02:00:38.600Z,33.9906667,-116.9925,5.54,0.68,ml,13,157,0.07259,0.12,ci,ci39917655,2022-01-20T16:32:04.777Z,"6km E of Calimesa, CA",earthquake,0.31,0.82,0.176,5,reviewed,ci,ci
2022-01-20T01:52:42.896Z,36.6565,-115.9988,0,-0.1,ml,9,265.06,0.073,0.1393,nn,nn00832090,2022-01-21T02:37:26.787Z,"30 km WNW of Indian Springs, Nevada",earthquake,,0,0.23,5,reviewed,nn,nn
2022-01-20T01:52:14.791Z,36.6578,-116.0051,0,0,ml,9,262.99,0.073,0.1339,nn,nn00832089,2022-01-21T02:37:25.855Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.28,4,reviewed,nn,nn
2022-01-20T01:46:56.728Z,38.1895,-117.7622,8.9,0.9,ml,8,217.56,0.12,0.1043,nn,nn00832006,2022-01-20T01:50:58.633Z,"37 km SE of Mina, Nevada",earthquake,,3.2,0.28,5,automatic,nn,nn
2022-01-20T01:40:14.860Z,38.8371658,-122.822998,1.88,0.94,md,23,80,0.009857,0.02,nc,nc73680826,2022-01-20T01:41:50.288Z,"9km NW of The Geysers, CA",earthquake,0.2,0.42,0.05,4,automatic,nc,nc
2022-01-20T01:38:25.250Z,46.3953333,-111.4856667,-2.95,1.03,ml,7,268,0.312,0.12,mb,mb80536464,2022-01-20T16:30:15.800Z,"7 km E of The Silos, Montana",earthquake,2.32,4.56,0.196,2,reviewed,mb,mb
2022-01-20T01:37:18.771Z,34.1908,51.7924,10,4.8,mb,,46,5.089,0.85,us,us7000gde3,2022-01-21T05:00:02.950Z,"97 km ESE of Qom, Iran",earthquake,7.8,1.9,0.057,97,reviewed,us,us
2022-01-20T01:35:34.740Z,33.1978333,-116.387,11.33,1.02,ml,53,50,0.07459,0.17,ci,ci39917639,2022-01-20T17:01:47.956Z,"7km S of Borrego Springs, CA",earthquake,0.16,0.3,0.13,23,reviewed,ci,ci
2022-01-20T01:33:24.170Z,35.953,-117.6633333,3.91,0.48,ml,12,101,0.01168,0.06,ci,ci39917647,2022-01-20T16:22:42.717Z,"22km E of Little Lake, CA",earthquake,0.17,0.21,0.033,4,reviewed,ci,ci
2022-01-20T01:28:19.616Z,-22.5121,-67.9811,185.37,4.3,mb,,70,0.474,0.41,us,us7000gde2,2022-01-21T04:38:37.040Z,"49 km NNE of San Pedro de Atacama, Chile",earthquake,9.1,11.7,0.189,8,reviewed,us,us
2022-01-20T01:22:46.914Z,36.67,-116.0017,0,-0.3,ml,9,257.32,0.06,0.1131,nn,nn00832088,2022-01-21T02:37:24.834Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.12,4,reviewed,nn,nn
2022-01-20T01:19:58.755Z,57.8238,-155.21,19.2,2.7,ml,,,,0.42,ak,ak022x3gkmc,2022-01-21T04:20:15.040Z,"53 km WNW of Karluk, Alaska",earthquake,,2.7,,,automatic,ak,ak
2022-01-20T01:19:32.974Z,36.6691,-116.0046,0,-0.2,ml,9,257.03,0.062,0.0976,nn,nn00832086,2022-01-21T02:37:23.917Z,"31 km WNW of Indian Springs, Nevada",earthquake,,0,0.42,5,reviewed,nn,nn
2022-01-20T01:13:24.190Z,39.4191667,-110.304,-2.17,1.86,md,6,198,0.01707,0.1,uu,uu60478207,2022-01-20T16:22:42.220Z,"16 km SSE of Sunnyside, Utah",earthquake,1.11,1.38,0.163,6,reviewed,uu,uu
2022-01-20T01:08:51.100Z,38.8330002,-122.8178329,1.15,0.36,md,7,115,0.01135,0.02,nc,nc73680816,2022-01-20T01:10:30.257Z,"8km NW of The Geysers, CA",earthquake,0.54,0.87,,1,automatic,nc,nc
2022-01-20T01:08:08.670Z,34.1523333,-80.7205,4.77,1.91,md,9,97,0.02618,0.21,se,se60143343,2022-01-21T22:04:35.034Z,"7 km ESE of Elgin, South Carolina",earthquake,0.82,0.84,0.048,7,reviewed,se,se
2022-01-20T01:05:01.910Z,36.015,-117.806,1.57,0.23,ml,8,75,0.03252,0.08,ci,ci37380452,2022-01-20T16:53:05.231Z,"13km NE of Little Lake, CA",earthquake,0.17,0.28,0.105,3,reviewed,ci,ci
2022-01-20T01:04:38.310Z,35.6956667,-117.5093333,11.54,0.68,ml,15,101,0.1155,0.1,ci,ci39917631,2022-01-20T16:45:27.854Z,"12km SW of Searles Valley, CA",earthquake,0.22,0.56,0.257,7,reviewed,ci,ci
2022-01-20T01:04:01.330Z,39.4163333,-110.2848333,-3.35,1.55,ml,9,204,0.03214,0.18,uu,uu60478202,2022-01-20T16:21:07.230Z,"17 km SSE of Sunnyside, Utah",earthquake,1.12,2.83,0.064,2,reviewed,uu,uu
2022-01-20T00:58:06.670Z,19.4273333333333,-155.5485,3.2,0.72,md,15,55,,0.1,hv,hv72000378,2022-01-20T07:18:36.010Z,"25 km NNW of Pāhala, Hawaii",earthquake,0.28,0.59,0.134445081645086,9,reviewed,hv,hv
2022-01-20T00:57:56.410Z,19.44,-155.535166666667,6.14,0.57,md,18,70,,0.11,hv,hv72000373,2022-01-20T06:32:56.390Z,"26 km NNW of Pāhala, Hawaii",earthquake,0.33,0.65,0.051100225110229,5,reviewed,hv,hv
2022-01-20T00:57:23.810Z,19.384,-155.621,5.78,1,md,18,132,,0.1,hv,hv72000348,2022-01-20T03:18:41.280Z,"25 km NW of Pāhala, Hawaii",earthquake,0.32,0.45,0.395905440248646,4,reviewed,hv,hv
2022-01-20T00:46:38.570Z,35.386,-84.6298333,5.09,2.05,md,14,77,0.05717,0.12,se,se60143443,2022-01-21T17:57:07.650Z,"5 km E of Riceville, Tennessee",earthquake,0.42,0.66,0.125,12,reviewed,se,se
2022-01-20T00:44:52.220Z,38.8089981,-122.7955017,3.73,0.34,md,7,112,0.00104,0.02,nc,nc73680811,2022-01-20T00:46:29.679Z,"5km NW of The Geysers, CA",earthquake,0.71,2.39,,1,automatic,nc,nc
2022-01-20T00:44:34.850Z,38.8233337,-122.7866669,0.87,1.16,md,22,40,0.01109,0.03,nc,nc73680806,2022-01-20T01:17:13.965Z,"6km W of Cobb, CA",earthquake,0.19,0.35,0.13,4,automatic,nc,nc
2022-01-20T00:43:32.269Z,63.7179,-149.2459,106.4,1.9,ml,,,,0.56,ak,ak022x308c0,2022-01-20T00:55:28.450Z,"16 km W of Denali Park, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-20T00:42:18.920Z,38.8240013,-122.7874985,0.81,0.97,md,20,57,0.01197,0.03,nc,nc73680801,2022-01-20T00:43:54.785Z,"6km W of Cobb, CA",earthquake,0.19,0.36,0.09,4,automatic,nc,nc
2022-01-20T00:38:31.780Z,35.703,-117.5128333,3.61,0.63,ml,14,101,0.1233,0.25,ci,ci39917623,2022-01-20T16:20:36.700Z,"12km SW of Searles Valley, CA",earthquake,0.56,31.61,0.091,3,reviewed,ci,ci
2022-01-20T00:37:04.740Z,38.8170013,-122.7981644,2.17,0.53,md,13,74,0.009293,0.02,nc,nc73680796,2022-01-20T00:38:39.699Z,"6km NW of The Geysers, CA",earthquake,0.32,0.6,0.37,2,automatic,nc,nc
2022-01-20T00:36:51.279Z,64.038,-148.7991,0,1.9,ml,,,,1.36,ak,ak022x2yrkv,2022-01-20T01:31:42.842Z,"15 km E of Ferry, Alaska",explosion,,0.3,,,automatic,ak,ak
2022-01-20T00:33:30.130Z,19.1813335418701,-155.488159179688,34.4000015258789,2.17000008,md,32,76,,0.119999997,hv,hv72882007,2022-01-20T00:36:35.260Z,"2 km SSW of Pāhala, Hawaii",earthquake,0.54,0.870000005,1.75,10,automatic,hv,hv
2022-01-20T00:26:32.940Z,44.5643333,-110.3755,4.18,0.58,md,11,73,0.01904,0.11,uu,uu60478197,2022-01-20T14:24:26.820Z,"52 km SSE of Mammoth, Wyoming",earthquake,0.31,0.44,0.352,8,reviewed,uu,uu
2022-01-20T00:24:32.962Z,63.0605,-149.4914,79.2,1.7,ml,,,,0.8,ak,ak022x2w5m0,2022-01-20T00:29:44.256Z,"45 km SW of Cantwell, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-20T00:24:23.910Z,35.0338333,-117.6741667,-0.78,1.65,ml,26,87,0.1009,0.16,ci,ci39917599,2022-01-20T17:47:19.243Z,"4km NNW of Boron, CA",quarry blast,0.38,31.61,0.162,25,reviewed,ci,ci
2022-01-20T00:21:24.610Z,38.7681656,-122.7263336,1.73,0.71,md,8,80,0.006663,0.01,nc,nc73680791,2022-01-20T00:23:00.349Z,"3km ESE of The Geysers, CA",earthquake,0.78,1.36,0.17,2,automatic,nc,nc
2022-01-20T00:20:14.840Z,19.1898326873779,-155.468994140625,34.8699989318848,1.87,md,36,101,,0.119999997,hv,hv72881997,2022-01-20T00:23:26.000Z,"1 km SE of Pāhala, Hawaii",earthquake,0.52,0.639999986,0.930000007,3,automatic,hv,hv
2022-01-20T00:09:59.274Z,36.678,-116.0062,0,-0.2,ml,7,255.96,0.053,0.0798,nn,nn00832084,2022-01-21T02:37:22.989Z,"32 km WNW of Indian Springs, Nevada",earthquake,,0,0.1,4,reviewed,nn,nn
2022-01-20T00:08:42.413Z,64.9966,-147.4817,0,1.3,ml,,,,0.61,ak,ak022x2sqvs,2022-01-20T00:39:35.689Z,"7 km ENE of Fox, Alaska",explosion,,0.6,,,automatic,ak,ak
2022-01-20T00:07:48.240Z,17.9581,-66.838,12,2.17,md,7,254,0.0446,0.07,pr,pr2022020000,2022-01-20T00:23:45.590Z,"4 km SSW of Indios, Puerto Rico",earthquake,0.73,0.42,0.09,5,reviewed,pr,pr
2022-01-19T23:55:05.960Z,38.8274994,-122.8125,2.12,0.85,md,8,74,0.004515,0.01,nc,nc73680786,2022-01-19T23:56:39.088Z,"7km NW of The Geysers, CA",earthquake,0.44,1.64,,1,automatic,nc,nc
2022-01-19T23:51:07.770Z,38.8288345,-122.8529968,1.37,0.87,md,16,71,0.00329,0.03,nc,nc73680781,2022-01-19T23:52:46.086Z,"10km NW of The Geysers, CA",earthquake,0.27,0.51,,1,automatic,nc,nc
2022-01-19T23:37:04.040Z,36.6741676,-121.2949982,3.98,1.68,md,19,138,0.04237,0.08,nc,nc73680776,2022-01-20T00:26:10.645Z,"13km S of Tres Pinos, CA",earthquake,0.32,1.01,0.21,17,automatic,nc,nc
2022-01-19T23:31:51.487Z,50.8871,-179.1049,14.53,4.2,mb,,212,0.691,0.87,us,us7000gddn,2022-01-20T00:37:59.040Z,"204 km WSW of Adak, Alaska",earthquake,4.1,5.7,0.101,27,reviewed,us,us
2022-01-19T23:24:23.031Z,50.8775,-179.0932,25.28,4.5,mb,,194,0.96,1.08,us,us7000gdcx,2022-01-20T00:06:20.806Z,"Andreanof Islands, Aleutian Islands, Alaska",earthquake,7.6,8.3,0.054,103,reviewed,us,us
2022-01-19T23:23:49.840Z,-20.8485,-175.4097,10,5,mb,,134,6.902,1.28,us,us7000gdcz,2022-01-21T02:35:05.040Z,"38 km NW of Nuku‘alofa, Tonga",earthquake,9.8,1.8,0.094,36,reviewed,us,us
2022-01-19T23:18:07.402Z,36.7067,-116.0132,2.8,-0.5,ml,7,214.87,0.031,0.1492,nn,nn00832005,2022-01-20T02:37:03.529Z,"34 km WNW of Indian Springs, Nevada",earthquake,,5.6,0.08,3,reviewed,nn,nn
2022-01-19T23:17:28.610Z,33.823,-116.9781667,12.57,0.3,ml,8,165,0.09816,0.08,ci,ci39917535,2022-01-20T00:36:12.815Z,"5km NNW of San Jacinto, CA",earthquake,0.36,0.95,0.068,3,reviewed,ci,ci
2022-01-19T23:17:27.745Z,61.4807,-149.913,31.9,1.8,ml,,,,0.61,ak,ak022vt09ln,2022-01-19T23:29:53.918Z,"5 km SSE of Big Lake, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-19T22:59:04.870Z,46.2658333333333,-119.3985,-0.26,1.88,ml,22,168,0.05447,0.12,uw,uw61802897,2022-01-20T17:05:32.073Z,"5 km SSW of West Richland, Washington",explosion,0.39,31.61,0.161295748879185,19,reviewed,uw,uw
2022-01-19T22:55:06.730Z,39.421,-110.3016667,-2.93,2.08,md,7,199,0.01841,0.14,uu,uu60478182,2022-01-20T16:14:55.300Z,"16 km SSE of Sunnyside, Utah",earthquake,1.19,2.92,0.145,6,reviewed,uu,uu
2022-01-19T22:54:52.441Z,60.0063,-152.9766,111.5,1.7,ml,,,,0.29,ak,ak022vsmtek,2022-01-19T22:58:19.903Z,"67 km ENE of Pedro Bay, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-19T22:54:43.992Z,48.4177,-71.7852,10,2.5,ml,,237,0.581,0.3,us,us7000gds6,2022-01-21T07:01:23.040Z,"0 km NNW of Metabetchouan-Lac-a-la-Croix, Canada",earthquake,3.1,2,0.091,16,reviewed,us,us
2022-01-19T22:42:35.870Z,32.7543333,-116.8011667,16.99,1.15,ml,25,91,0.06414,0.16,ci,ci39917479,2022-01-19T22:54:04.840Z,"8km ENE of Jamul, CA",earthquake,0.29,0.53,0.19,11,reviewed,ci,ci
2022-01-19T22:42:14.340Z,39.4215,-110.3056667,-2.04,2.06,md,8,197,0.01527,0.14,uu,uu60478177,2022-01-20T16:13:51.020Z,"16 km SSE of Sunnyside, Utah",earthquake,1.29,1.4,0.17,7,reviewed,uu,uu
2022-01-19T22:41:33.140Z,38.8351669,-122.7893295,1.97,0.85,md,10,83,0.003333,0.01,nc,nc73680771,2022-01-19T22:43:10.461Z,"6km WNW of Cobb, CA",earthquake,0.48,1.01,,1,automatic,nc,nc
2022-01-19T22:40:01.940Z,44.4381667,-111.4098333,7.72,1.34,ml,24,135,0.11,0.29,mb,mb80536479,2022-01-20T17:01:59.660Z,"3 km WNW of Island Park, Idaho",earthquake,0.51,1.24,0.151,14,reviewed,mb,mb
2022-01-19T22:39:50.278Z,-3.3257,137.7045,70.81,4.5,mb,,87,5.462,0.81,us,us7000gdck,2022-01-19T22:59:50.040Z,"244 km E of Nabire, Indonesia",earthquake,13.3,9.6,0.171,10,reviewed,us,us
2022-01-19T22:39:26.230Z,34.9826667,-118.1811667,-0.82,1.16,ml,17,63,0.1107,0.19,ci,ci39917463,2022-01-19T22:47:53.683Z,"8km S of Mojave, CA",quarry blast,0.43,31.61,0.154,15,reviewed,ci,ci
2022-01-19T22:22:31.097Z,36.7091,-115.8771,0,1,ml,15,272.31,0.089,0.1304,nn,nn00831980,2022-01-20T02:36:54.650Z,"24 km NW of Indian Springs, Nevada",earthquake,,0,0.29,8,reviewed,nn,nn
2022-01-19T22:10:43.440Z,49.3526666666667,-120.485,-0.37,2.05,ml,14,178,0.5631,0.28,uw,uw61802872,2022-01-20T20:00:33.760Z,"11 km S of Princeton, Canada",explosion,1.56,31.61,0.165452014905357,8,reviewed,uw,uw
2022-01-19T22:02:24.493Z,-21.5368,-68.4608,130.68,4.2,mb,,55,1.076,0.65,us,us7000gdc4,2022-01-19T22:30:26.040Z,"112 km NNE of Calama, Chile",earthquake,5.5,7.3,0.146,13,reviewed,us,us
2022-01-19T22:01:36.348Z,36.943,-116.088,5.6,0.4,ml,15,64.43,0.028,0.1313,nn,nn00832003,2022-01-20T02:37:02.579Z,"55 km NW of Indian Springs, Nevada",earthquake,,1.2,0.32,9,reviewed,nn,nn
2022-01-19T21:58:06.965Z,36.671,-116.0004,0,-0.2,ml,8,265.08,0.059,0.0969,nn,nn00832002,2022-01-20T02:37:01.354Z,"California-Nevada border region",earthquake,,0,0.08,4,reviewed,nn,nn
2022-01-19T21:52:37.901Z,32.3697,105.289,10,4.4,mb,,55,4.159,0.77,us,us7000gdcd,2022-01-20T19:43:45.880Z,"50 km W of Guangyuan, China",earthquake,5.8,1.9,0.084,41,reviewed,us,us
2022-01-19T21:48:52.106Z,62.8196,-149.591,50.1,1.6,ml,,,,0.99,ak,ak022vs03h6,2022-01-19T22:17:55.308Z,"48 km NNE of Chase, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-19T21:48:46.980Z,19.1663341522217,-155.498168945312,29.9799995422363,1.72000003,md,30,146,,0.140000001,hv,hv72881852,2022-01-19T21:51:52.110Z,"4 km SSW of Pāhala, Hawaii",earthquake,0.96,0.769999981,1.72000003,4,automatic,hv,hv
2022-01-19T21:42:26.500Z,35.8586667,-117.6615,6.45,-0.26,ml,5,125,0.06737,0.1,ci,ci39917375,2022-01-19T22:21:32.503Z,"24km ESE of Little Lake, CA",earthquake,0.54,1.69,0.157,2,reviewed,ci,ci
2022-01-19T21:37:30.954Z,59.5631,-138.919,6.8,2.2,ml,,,,0.86,ak,ak022vrxoyv,2022-01-19T21:42:01.386Z,"45 km E of Yakutat, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-19T21:29:05.273Z,63.1055,-151.3574,1.5,2,ml,,,,0.69,ak,ak022vrvx9b,2022-01-19T21:42:01.248Z,"51 km SSE of Denali National Park, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-19T21:28:20.724Z,61.1568,-149.4912,18.9,1.4,ml,,,,0.69,ak,ak022vrvpiv,2022-01-19T22:24:36.171Z,"13 km SE of Elmendorf Air Force Base, Alaska",earthquake,,0.3,,,reviewed,ak,ak
2022-01-19T21:27:30.222Z,-37.4117,-74.2157,6.97,4.8,mwr,,139,1.054,0.83,us,us7000gdbn,2022-01-19T23:11:31.040Z,"54 km WNW of Lebu, Chile",earthquake,4.9,3.3,,,reviewed,us,guc
2022-01-19T21:27:14.160Z,44.6718333,-110.0598333,10.84,1.07,md,8,89,0.09681,0.19,uu,uu60478152,2022-01-19T22:31:25.680Z,"37 km S of Silver Gate, Montana",earthquake,0.65,1.49,0.278,5,reviewed,uu,uu
2022-01-19T21:27:06.860Z,44.6676667,-110.4713333,4.7,0.69,md,5,184,0.05336,0.16,uu,uu60029859,2022-01-19T22:33:00.600Z,"38 km SSE of Mammoth, Wyoming",earthquake,0.64,1.46,0.467,2,reviewed,uu,uu
2022-01-19T21:26:58.050Z,44.6655,-110.4698333,2.57,-0.19,md,4,184,0.05577,0.18,uu,uu60029864,2022-01-19T22:35:06.430Z,"39 km SSE of Mammoth, Wyoming",earthquake,2.47,9.72,0.173,2,reviewed,uu,uu
2022-01-19T21:26:48.481Z,39.4045,-119.7782,7,0.6,ml,15,93.13,0.027,0.1565,nn,nn00832001,2022-01-20T02:37:00.439Z,"14 km SSE of Reno, Nevada",earthquake,,1.4,0.22,7,reviewed,nn,nn
2022-01-19T21:13:40.810Z,38.8458328,-122.8166656,1.12,0.81,md,17,60,0.01024,0.02,nc,nc73680761,2022-01-19T21:15:14.415Z,"8km WNW of Cobb, CA",earthquake,0.22,0.43,0.25,3,automatic,nc,nc
2022-01-19T21:03:14.220Z,33.4786667,-116.7855,4.75,1.61,ml,53,27,0.03583,0.19,ci,ci39917303,2022-01-19T21:22:56.440Z,"8km ENE of Aguanga, CA",earthquake,0.17,0.89,0.095,27,reviewed,ci,ci
2022-01-19T21:00:49.740Z,38.7906685,-122.7343369,1.95,0.66,md,11,122,0.007652,0.01,nc,nc73680751,2022-01-19T21:02:24.436Z,"2km NE of The Geysers, CA",earthquake,0.35,0.69,0.5,3,automatic,nc,nc
2022-01-19T21:00:29.670Z,32.7531667,-116.9108333,5.07,1.36,ml,18,84,0.03185,0.16,ci,ci39917295,2022-01-19T22:10:53.551Z,"2km ENE of Rancho San Diego, CA",quarry blast,0.7,1.14,0.164,9,reviewed,ci,ci
2022-01-19T20:59:51.930Z,46.1966666666667,-122.192333333333,2.67,0.08,ml,9,90,0.005918,0.07,uw,uw61802847,2022-01-20T01:40:31.320Z,"37 km NNE of Amboy, Washington",earthquake,0.49,0.51,0.0359545523088696,3,reviewed,uw,uw
2022-01-19T20:59:39.520Z,38.9545,-123.0573333,4.14,2.13,md,55,71,0.04065,0.09,nc,nc73680746,2022-01-22T01:46:11.122Z,"16km SW of Lakeport, CA",earthquake,0.17,0.3,0.138,31,reviewed,nc,nc
2022-01-19T20:59:38.970Z,19.1783332824707,-155.495330810547,34.8400001525879,2.1,ml,41,138,,0.119999997,hv,hv72881787,2022-01-19T21:05:25.860Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.57,0.769999981,3.96,9,automatic,hv,hv
2022-01-19T20:54:05.590Z,45.0708333,-111.85,13.79,0.83,ml,12,137,0.211,0.18,mb,mb80536474,2022-01-20T16:44:27.400Z,"25 km SSE of Virginia City, Montana",earthquake,0.72,1.52,0.101,4,reviewed,mb,mb
2022-01-19T20:53:26.230Z,39.2951667,-111.9005,14.04,1.37,md,7,104,0.2188,0.11,uu,uu60478142,2022-01-20T15:52:46.710Z,"8 km NNW of Fayette, Utah",earthquake,0.67,1.53,0.524,3,reviewed,uu,uu
2022-01-19T20:47:40.870Z,33.3355,-116.3478333,11.9,0.95,ml,28,160,0.01838,0.15,ci,ci39917271,2022-01-19T22:05:56.766Z,"9km NNE of Borrego Springs, CA",earthquake,0.26,0.52,0.139,19,reviewed,ci,ci
2022-01-19T20:42:36.030Z,45.0676667,-111.839,11.71,1.37,ml,19,96,0.219,0.16,mb,mb80536414,2022-01-19T21:09:44.420Z,"26 km SSE of Virginia City, Montana",earthquake,0.45,1.46,0.157,6,reviewed,mb,mb
2022-01-19T20:31:04.410Z,39.419,-110.306,-2.09,1.44,md,7,197,0.01565,0.12,uu,uu60478132,2022-01-20T15:47:37.260Z,"16 km SSE of Sunnyside, Utah",earthquake,1.06,1.22,0.147,6,reviewed,uu,uu
2022-01-19T20:31:00.960Z,38.8358345,-122.8193359,1.63,0.85,md,11,68,0.01291,0.01,nc,nc73680731,2022-01-19T20:32:34.716Z,"8km W of Cobb, CA",earthquake,0.3,0.76,,1,automatic,nc,nc
2022-01-19T20:18:48.040Z,19.1736660003662,-155.476837158203,34.0800018310547,2.19,ml,48,77,,0.100000001,hv,hv72881737,2022-01-19T20:24:18.190Z,"3 km S of Pāhala, Hawaii",earthquake,0.44,0.589999974,4.02,16,automatic,hv,hv
2022-01-19T20:18:44.440Z,35.624,-117.4706667,7.03,1.07,ml,19,109,0.03805,0.09,ci,ci39917199,2022-01-19T22:01:05.732Z,"17km SSW of Searles Valley, CA",earthquake,0.19,0.35,0.124,9,reviewed,ci,ci
2022-01-19T20:18:36.990Z,18.8366,-64.3845,17,4.01,md,28,210,1.0423,0.37,pr,pr2022019009,2022-01-20T15:03:07.282Z,"70 km NE of Cruz Bay, U.S. Virgin Islands",earthquake,2.32,3.04,0.09,22,reviewed,pr,pr
2022-01-19T20:18:10.396Z,-20.5931,-175.4137,10,4.6,mb,,124,6.793,0.68,us,us7000gdqq,2022-01-21T03:05:00.040Z,"64 km NNW of Nuku‘alofa, Tonga",earthquake,7.5,1.9,0.142,15,reviewed,us,us
2022-01-19T20:12:00.420Z,19.1648333333333,-155.5025,34.11,1.62,md,20,167,,0.11,hv,hv72881727,2022-01-19T22:40:50.680Z,"4 km SSW of Pāhala, Hawaii",earthquake,0.61,0.69,0.0978716507299582,11,reviewed,hv,hv
2022-01-19T20:11:11.260Z,35.0568333,-118.3436667,-0.84,1.17,ml,19,89,0.0661,0.15,ci,ci39917191,2022-01-19T21:58:48.287Z,"13km SE of Tehachapi, CA",quarry blast,0.37,31.61,0.092,19,reviewed,ci,ci
2022-01-19T20:10:04.070Z,32.9263333,-115.984,9.99,1.14,ml,18,107,0.04133,0.16,ci,ci39917183,2022-01-19T22:19:27.519Z,"21km N of Ocotillo, CA",earthquake,0.29,0.61,0.173,15,reviewed,ci,ci
2022-01-19T20:10:01.140Z,34.4408333,-117.7408333,5.3,1.02,ml,14,134,0.07824,0.18,ci,ci39917175,2022-01-19T22:16:23.298Z,"7km SE of Llano, CA",earthquake,0.43,0.97,0.139,11,reviewed,ci,ci
2022-01-19T20:08:15.990Z,34.4391667,-117.7375,6.04,0.84,ml,11,155,0.07517,0.11,ci,ci39917167,2022-01-19T22:24:06.934Z,"8km SE of Llano, CA",earthquake,0.36,0.58,0.172,11,reviewed,ci,ci
2022-01-19T20:07:56.460Z,63.2416,-144.8006,0,1.4,ml,,,,0.97,ak,ak022vr5vub,2022-01-19T20:37:34.541Z,"44 km ENE of Paxson, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-19T20:04:45.140Z,33.4461667,-116.5443333,10.37,2.09,ml,87,16,0.06843,0.19,ci,ci39917159,2022-01-20T04:38:47.950Z,"17km SE of Anza, CA",earthquake,0.12,0.23,0.169,77,reviewed,ci,ci
2022-01-19T20:03:51.010Z,45.999,-112.4726667,-2,1.71,ml,15,166,0.059,0.12,mb,mb80536409,2022-01-19T21:18:05.440Z,"4 km E of Butte, Montana",quarry blast,0.6,31.61,0.212,7,reviewed,mb,mb
2022-01-19T19:59:00.650Z,33.4506667,-116.534,10.44,0.15,ml,11,100,0.07196,0.13,ci,ci39917151,2022-01-20T21:05:53.901Z,"17km SE of Anza, CA",earthquake,0.44,0.83,0.17,3,reviewed,ci,ci
2022-01-19T19:51:53.130Z,18.0956,-66.8871,16,2.33,md,13,56,0.1208,0.26,pr,pr2022019008,2022-01-19T20:07:15.188Z,"6 km NNE of Lluveras, Puerto Rico",earthquake,0.49,0.95,0.21,7,reviewed,pr,pr
2022-01-19T19:28:51.870Z,38.824501,-122.7519989,0.01,0.91,md,10,146,0.01521,0.03,nc,nc73680701,2022-01-19T19:30:29.497Z,"2km W of Cobb, CA",earthquake,0.32,0.84,0.31,2,automatic,nc,nc
2022-01-19T19:25:14.290Z,46.3105,-111.62,-2,1.15,ml,6,165,0.328,0.17,mb,mb80536459,2022-01-20T16:23:00.100Z,"7 km W of Townsend, Montana",quarry blast,1.33,31.61,0.128,4,reviewed,mb,mb
2022-01-19T19:21:09.560Z,51.847,-177.789333333333,-1.77,0.19,ml,4,272,,0.11,av,av91047463,2022-01-21T07:42:57.490Z,"79 km W of Adak, Alaska",earthquake,2.16,2.84,0.105854418678353,4,reviewed,av,av
2022-01-19T19:21:00.390Z,45.0698333,-111.8485,11.7,2.85,ml,58,56,0.213,0.23,mb,mb80536404,2022-01-19T19:53:39.550Z,"26 km SSE of Virginia City, Montana",earthquake,0.37,0.63,0.167,28,reviewed,mb,mb
2022-01-19T19:18:43.720Z,38.7896652,-122.7606659,1.58,0.95,md,15,77,0.01933,0.04,nc,nc73680696,2022-01-19T19:20:19.295Z,"1km NNW of The Geysers, CA",earthquake,0.28,0.58,0.19,3,automatic,nc,nc
2022-01-19T19:14:54.160Z,36.1011667,-91.1868333,0.06,2.09,md,12,83,0.04092,0.2,nm,nm60143348,2022-01-20T14:36:18.550Z,"6 km WNW of Powhatan, Arkansas",earthquake,0.52,1.84,0.055,5,reviewed,nm,nm
2022-01-19T19:11:19.740Z,33.9923333,-116.9803333,4.51,0.98,ml,36,78,0.06561,0.16,ci,ci39917063,2022-01-19T21:48:47.726Z,"7km E of Calimesa, CA",earthquake,0.21,0.46,0.183,15,reviewed,ci,ci
2022-01-19T19:11:12.495Z,62.5528,-151.187,84.8,1.9,ml,,,,0.83,ak,ak022vql7p7,2022-01-19T19:22:36.642Z,"22 km WNW of Petersville, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-19T19:10:54.650Z,33.9911667,-116.9896667,4.92,0.37,ml,7,222,0.0708,0.16,ci,ci37379964,2022-01-19T21:41:45.607Z,"6km E of Calimesa, CA",earthquake,0.83,1.83,0.225,2,reviewed,ci,ci
2022-01-19T19:10:28.040Z,33.9895,-116.9771667,3.45,0.82,ml,19,150,0.06682,0.1,ci,ci39917055,2022-01-19T21:35:33.776Z,"7km N of Beaumont, CA",earthquake,0.28,0.61,0.152,12,reviewed,ci,ci
2022-01-19T19:09:47.560Z,35.9251667,-117.6726667,3.82,0.31,ml,14,67,0.02901,0.21,ci,ci39917071,2022-01-20T19:55:41.225Z,"21km E of Little Lake, CA",earthquake,0.32,0.65,0.033,6,reviewed,ci,ci
2022-01-19T19:06:30.870Z,36.6663322,-121.3016663,3.16,1.37,md,6,172,0.05176,0.03,nc,nc73680691,2022-01-19T19:42:11.135Z,"14km S of Tres Pinos, CA",earthquake,0.56,1.37,0.18,7,automatic,nc,nc
2022-01-19T19:05:49.130Z,35.9713333,-117.4226667,7.68,0.48,ml,7,149,0.1387,0.08,ci,ci37379868,2022-01-19T21:30:46.540Z,"23km N of Searles Valley, CA",earthquake,0.29,1.39,0.132,3,reviewed,ci,ci
2022-01-19T19:05:41.080Z,35.9715,-117.3966667,4.52,0.81,ml,13,158,0.1222,0.12,ci,ci39917039,2022-01-19T21:27:59.267Z,"23km N of Searles Valley, CA",earthquake,0.31,0.8,0.191,5,reviewed,ci,ci
2022-01-19T18:59:53.601Z,61.7605,-149.4838,36.3,1.5,ml,,,,0.67,ak,ak022vqa5nk,2022-01-19T19:02:54.076Z,"13 km W of Fishhook, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-19T18:59:36.180Z,39.4235,-110.3043333,-2.26,1.75,ml,12,182,0.0161,0.16,uu,uu60478117,2022-01-19T19:40:03.090Z,"15 km SSE of Sunnyside, Utah",earthquake,0.5,1.45,0.099,3,reviewed,uu,uu
2022-01-19T18:52:57.610Z,32.9311667,-115.9838333,10.21,0.89,ml,14,194,0.04591,0.17,ci,ci39917015,2022-01-19T19:00:01.456Z,"22km N of Ocotillo, CA",earthquake,0.49,0.68,0.226,10,reviewed,ci,ci
2022-01-19T18:43:12.336Z,38.1743,-117.9696,2.6,1.1,ml,15,113.31,0.028,0.1482,nn,nn00831947,2022-01-19T20:35:48.265Z,"26 km SSE of Mina, Nevada",earthquake,,0.9,0.75,4,reviewed,nn,nn
2022-01-19T18:43:09.175Z,59.9343,-151.863,81.6,1.4,ml,,,,0.38,ak,ak022vq6mrn,2022-01-19T18:49:12.525Z,"7 km W of Happy Valley, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-19T18:39:58.000Z,38.8288345,-122.8115005,1.48,1.07,md,16,62,0.005545,0.01,nc,nc73680686,2022-01-19T18:41:33.439Z,"8km NW of The Geysers, CA",earthquake,0.2,0.57,0.13,2,automatic,nc,nc
2022-01-19T18:39:35.430Z,19.1644992828369,-155.492340087891,32.2900009155273,1.78999996,md,31,109,,0.150000006,hv,hv72881627,2022-01-19T18:42:52.240Z,"4 km SSW of Pāhala, Hawaii",earthquake,0.69,1.24000001,1.24000001,8,automatic,hv,hv
2022-01-19T18:35:00.862Z,60.111,-153.0169,121.1,2.4,ml,,,,0.89,ak,ak022vq4web,2022-01-19T18:38:41.077Z,"70 km ENE of Pedro Bay, Alaska",earthquake,,2.1,,,automatic,ak,ak
2022-01-19T18:29:35.980Z,19.2251666666667,-155.443666666667,34.21,1.51,md,21,121,,0.13,hv,hv72881607,2022-01-20T01:43:37.670Z,"4 km NE of Pāhala, Hawaii",earthquake,0.54,0.63,0.0536879237098554,10,reviewed,hv,hv
2022-01-19T18:28:21.390Z,39.2916667,-122.791,8.46,1.8,md,21,81,0.1468,0.16,nc,nc73680681,2022-01-19T23:33:11.346Z,"18km NE of Upper Lake, CA",earthquake,0.28,1.28,0.136,20,reviewed,nc,nc
2022-01-19T18:26:20.681Z,64.5503,-149.3683,18.3,1.1,ml,,,,0.2,ak,ak022vq30hg,2022-01-19T18:30:30.137Z,"13 km W of Nenana, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-19T18:22:17.431Z,-20.7456,-175.436,10,4.8,mb,,124,6.836,0.32,us,us7000gdqu,2022-01-21T03:28:07.040Z,"49 km NNW of Nuku‘alofa, Tonga",earthquake,7,1.9,0.138,16,reviewed,us,us
2022-01-19T18:08:14.403Z,62.2006,-150.5662,7.7,1.1,ml,,,,0.83,ak,ak022vpz02r,2022-01-19T20:37:34.297Z,"21 km SW of Trapper Creek, Alaska",earthquake,,0.2,,,reviewed,ak,ak
2022-01-19T18:07:56.890Z,45.398,-112.5521667,2.98,0.8,ml,6,133,0.047,0.06,mb,mb80536469,2022-01-20T16:34:34.040Z,"21 km NNE of Dillon, Montana",earthquake,0.64,0.91,0.373,3,reviewed,mb,mb
2022-01-19T18:02:07.890Z,34.0106667,-117.1158333,8.99,1.35,ml,43,81,0.0249,0.16,ci,ci39916927,2022-01-19T18:55:58.901Z,"6km WNW of Calimesa, CA",earthquake,0.19,0.52,0.154,22,reviewed,ci,ci
2022-01-19T18:00:22.040Z,-25.2555,179.6155,534.29,4.5,mb,,78,7.613,0.82,us,us7000gd8b,2022-01-19T18:22:43.040Z,"south of the Fiji Islands",earthquake,15.5,10.7,0.124,19,reviewed,us,us
2022-01-19T17:56:42.000Z,38.8476677,-122.8033371,1.8,0.37,md,9,69,0.008657,0.01,nc,nc73680671,2022-01-19T17:58:18.716Z,"8km WNW of Cobb, CA",earthquake,0.35,1.03,,1,automatic,nc,nc
2022-01-19T17:56:30.250Z,38.8478317,-122.8164978,1.54,0.37,md,7,92,0.008667,0.01,nc,nc73680666,2022-01-19T17:58:09.226Z,"9km WNW of Cobb, CA",earthquake,0.37,1.47,,1,automatic,nc,nc
2022-01-19T17:53:21.460Z,60.6035,-150.9066,21.5,1.9,ml,,,,0.82,ak,ak022vpndcq,2022-01-19T17:57:36.636Z,"10 km NW of Sterling, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-19T17:52:36.120Z,38.1788,-117.8771,10.8,1.6,ml,17,112.51,0.076,0.1387,nn,nn00831942,2022-01-19T18:25:35.115Z,"31 km SE of Mina, Nevada",earthquake,,1.1,0.21,7,reviewed,nn,nn
2022-01-19T17:48:56.080Z,19.1648330688477,-155.47917175293,33.6199989318848,2.07999992,md,38,101,,0.119999997,hv,hv72881562,2022-01-19T17:52:10.890Z,"4 km S of Pāhala, Hawaii",earthquake,0.64,0.899999976,1.03999996,11,automatic,hv,hv
2022-01-19T17:46:28.940Z,33.5826667,-116.8118333,5.87,2.18,ml,72,20,0.04133,0.2,ci,ci39916895,2022-01-20T04:37:54.634Z,"13km WNW of Anza, CA",earthquake,0.17,0.48,0.19,25,reviewed,ci,ci
2022-01-19T17:44:28.410Z,35.9688333,-117.3916667,2.89,1.76,ml,30,68,0.1174,0.13,ci,ci39916887,2022-01-19T18:54:40.358Z,"22km N of Searles Valley, CA",earthquake,0.21,0.7,0.143,22,reviewed,ci,ci
2022-01-19T17:43:48.590Z,44.8025,-110.8158333,8.05,0.64,md,13,106,0.02846,0.13,uu,uu60478097,2022-01-19T18:02:02.110Z,"Wyoming",earthquake,0.71,0.74,0.349,8,reviewed,uu,uu
2022-01-19T17:43:44.080Z,19.2083339691162,-155.42366027832,33.189998626709,2.27,ml,39,147,,0.180000007,hv,hv72881557,2022-01-19T17:49:14.790Z,"5 km E of Pāhala, Hawaii",earthquake,0.81,0.970000029,0.17,5,automatic,hv,hv
2022-01-19T17:30:41.880Z,32.9205,-115.9881667,9.43,1.84,ml,51,33,0.03719,0.2,ci,ci39916863,2022-01-19T18:50:27.900Z,"21km N of Ocotillo, CA",earthquake,0.19,0.52,0.133,41,reviewed,ci,ci
2022-01-19T17:20:51.820Z,34.0053333,-117.1735,12.3,0.6,ml,16,168,0.1317,0.14,ci,ci39916855,2022-01-19T19:03:07.632Z,"6km S of Redlands, CA",earthquake,0.43,1.19,0.105,9,reviewed,ci,ci
2022-01-19T17:04:12.192Z,63.0567,-149.8931,74.4,2,ml,,,,0.46,ak,ak022vpcuh2,2022-01-19T17:18:41.967Z,"60 km SW of Cantwell, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-19T17:01:26.040Z,44.7841667,-110.8156667,5.34,0.72,md,10,205,0.02515,0.14,uu,uu60478092,2022-01-19T17:11:38.030Z,"23 km SSW of Mammoth, Wyoming",earthquake,1.17,1.38,0.362,6,reviewed,uu,uu
2022-01-19T16:56:50.590Z,47.4376666666667,-122.6625,27.93,0.83,ml,7,233,0.139,0.3,uw,uw61802737,2022-01-20T01:46:23.690Z,"3 km NW of Burley, Washington",earthquake,1.32,2.22,0.110985257430073,3,reviewed,uw,uw
2022-01-19T16:56:21.950Z,19.181999206543,-155.483505249023,2.53999996185303,2.45,ml,20,125,,0.379999995,hv,hv72881472,2022-01-19T17:01:54.730Z,"2 km SSW of Pāhala, Hawaii",earthquake,1.92,3.77999997,5.32,3,automatic,hv,hv
2022-01-19T16:56:15.570Z,19.1693333333333,-155.472666666667,33.79,2.9,ml,51,80,,0.11,hv,hv72881482,2022-01-21T06:28:19.040Z,"3 km S of Pāhala, Hawaii",earthquake,0.45,0.55,0.150611065723634,35,reviewed,hv,hv
2022-01-19T16:55:58.490Z,19.1848333333333,-155.471666666667,33.39,1.59,md,21,104,,0.09,hv,hv72881477,2022-01-19T22:01:03.550Z,"2 km SSE of Pāhala, Hawaii",earthquake,0.73,0.67,0.110256853920644,12,reviewed,hv,hv
2022-01-19T16:50:02.170Z,35.9708333,-117.3866667,1.39,1.14,ml,17,161,0.1157,0.13,ci,ci37487733,2022-01-19T18:27:08.971Z,"23km N of Searles Valley, CA",earthquake,0.35,0.44,0.067,6,reviewed,ci,ci
2022-01-19T16:49:46.010Z,35.9685,-117.3911667,2.63,1.59,ml,26,68,0.1168,0.12,ci,ci39916775,2022-01-19T18:22:44.874Z,"22km N of Searles Valley, CA",earthquake,0.2,0.44,0.097,16,reviewed,ci,ci
2022-01-19T16:36:45.940Z,35.6408333,-117.5645,8.5,0.93,ml,20,80,0.08994,0.13,ci,ci39916751,2022-01-19T18:15:46.423Z,"10km ENE of Ridgecrest, CA",earthquake,0.19,0.58,0.093,11,reviewed,ci,ci
2022-01-19T16:20:49.300Z,38.7806664,-122.7648315,0.99,0.46,md,10,101,0.009957,0.02,nc,nc73680641,2022-01-19T16:22:27.482Z,"1km WNW of The Geysers, CA",earthquake,0.32,0.65,0.4,2,automatic,nc,nc
2022-01-19T16:19:48.610Z,33.6136667,-116.6461667,15.64,0.47,ml,20,76,0.04462,0.15,ci,ci39916743,2022-01-19T18:10:39.256Z,"7km NNE of Anza, CA",earthquake,0.38,0.5,0.074,6,reviewed,ci,ci
2022-01-19T16:18:57.940Z,39.4176667,-110.2931667,-3.39,1.67,md,7,185,0.02556,0.12,uu,uu60478087,2022-01-19T17:06:23.030Z,"16 km SSE of Sunnyside, Utah",earthquake,1.28,3.07,0.143,6,reviewed,uu,uu
2022-01-19T16:18:33.979Z,59.927,-153.4751,147.8,1.9,ml,,,,0.77,ak,ak022vougi5,2022-01-19T16:24:15.924Z,"38 km ENE of Pedro Bay, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-19T15:58:04.500Z,35.901,-117.7328333,10.33,0.69,ml,12,57,0.08166,0.1,ci,ci39916711,2022-01-19T16:33:22.080Z,"16km ESE of Little Lake, CA",earthquake,0.2,0.44,0.14,4,reviewed,ci,ci
2022-01-19T15:57:44.952Z,61.9158,-149.2912,33.9,1.4,ml,,,,0.51,ak,ak022voheqn,2022-01-19T16:02:23.478Z,"19 km N of Fishhook, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-19T15:57:34.430Z,41.8956667,-112.5746667,1.89,0.75,md,7,136,0.1893,0.04,uu,uu60478082,2022-01-19T17:04:48.000Z,"13 km SE of Snowville, Utah",earthquake,0.52,31.61,0.193,6,reviewed,uu,uu
2022-01-19T15:53:27.319Z,-4.5725,124.0524,11.01,4.9,mb,,61,3.733,0.69,us,us7000gd5y,2022-01-19T16:32:46.040Z,"174 km ENE of Katabu, Indonesia",earthquake,7.7,4.4,0.11,26,reviewed,us,us
2022-01-19T15:46:40.100Z,54.1723333333333,-165.9945,4.47,-0.87,ml,5,118,,0.05,av,av91047458,2022-01-21T07:29:34.470Z,"14 km WNW of Akutan, Alaska",earthquake,0.38,0.85,0.290054174324852,5,reviewed,av,av
2022-01-19T15:35:53.220Z,-3.5392,130.9959,10,4.4,mb,,75,1.394,1.11,us,us7000gd5w,2022-01-20T00:37:05.040Z,"231 km E of Amahai, Indonesia",earthquake,4.2,1.9,0.117,21,reviewed,us,us
2022-01-19T15:35:09.137Z,61.1321,-150.0892,37.6,2,ml,,,,0.69,ak,ak022vocm6x,2022-01-19T15:48:11.920Z,"13 km SW of Anchorage, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-19T15:22:13.800Z,19.2210006713867,-155.408828735352,32.1500015258789,2.36,ml,50,142,,0.159999996,hv,hv72881402,2022-01-19T23:54:55.040Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.54,0.74000001,4.05,20,automatic,hv,hv
2022-01-19T15:01:17.230Z,19.2151660919189,-155.416839599609,33.4500007629395,2.28,ml,41,141,,0.140000001,hv,hv72881397,2022-01-19T15:06:47.670Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.47,0.730000019,0.37,3,automatic,hv,hv
2022-01-19T14:58:06.018Z,-30.6638,-72.3184,10,4.1,mwr,,190,0.588,0.44,us,us7000gd5q,2022-01-21T14:44:00.040Z,"107 km W of Ovalle, Chile",earthquake,4.4,1.9,0.044,50,reviewed,us,us
2022-01-19T14:52:03.560Z,44.5905,-110.7271667,8.56,0.54,md,8,99,0.06181,0.15,uu,uu60478077,2022-01-19T16:54:29.780Z,"30 km ESE of West Yellowstone, Montana",earthquake,0.64,1.28,0.365,7,reviewed,uu,uu
2022-01-19T14:50:33.471Z,60.7932,-152.0338,93.9,1.1,ml,,,,0.56,ak,ak022vnug8j,2022-01-19T15:05:27.070Z,"42 km WNW of Nikiski, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-19T14:49:51.310Z,35.8558333,-119.8108333,7.42,1.83,md,35,112,0.2287,0.24,nc,nc73680636,2022-01-21T01:36:11.519Z,"22km SE of Kettleman City, CA",earthquake,0.56,1.27,0.127,30,reviewed,nc,nc
2022-01-19T14:49:40.692Z,39.4112,-120.2145,8.7,-0.2,ml,4,170.74,0.101,0.0248,nn,nn00831999,2022-01-20T02:36:56.654Z,"9 km NNW of Truckee, California",earthquake,,5.1,0.32,3,reviewed,nn,nn
2022-01-19T14:48:11.610Z,35.8323333,-119.7948333,10.85,2,md,35,132,0.2216,0.23,nc,nc73680631,2022-01-19T19:14:10.950Z,"25km SE of Kettleman City, CA",earthquake,0.52,1.12,0.12,33,reviewed,nc,nc
2022-01-19T14:47:57.520Z,-7.77,118.4432,8.12,4.7,mb,,80,3.03,0.43,us,us7000gd5p,2022-01-19T15:05:31.040Z,"82 km NNW of Bima, Indonesia",earthquake,5.4,5.7,0.143,15,reviewed,us,us
2022-01-19T14:44:35.820Z,19.2036666870117,-155.449005126953,36.0999984741211,1.82000005,md,42,121,,0.109999999,hv,hv72881392,2022-01-19T14:47:38.110Z,"3 km E of Pāhala, Hawaii",earthquake,0.59,0.839999974,0.560000002,11,automatic,hv,hv
2022-01-19T14:38:39.099Z,-20.5917,-175.3746,10,4.8,mb,,136,6.826,0.98,us,us7000ge5m,2022-01-22T05:23:07.040Z,"63 km NNW of Nuku‘alofa, Tonga",earthquake,7.3,1.9,0.135,17,reviewed,us,us
2022-01-19T14:35:10.830Z,35.6948333,-121.022,4.72,0.97,md,19,80,0.1079,0.03,nc,nc73680626,2022-01-21T23:48:36.381Z,"13km WSW of Lake Nacimiento, CA",earthquake,0.32,1.22,0.185,9,reviewed,nc,nc
2022-01-19T14:29:43.645Z,-3.5158,130.8974,9.3,5.3,mww,,64,1.473,0.8,us,us7000gd5g,2022-01-20T14:33:15.339Z,"220 km E of Amahai, Indonesia",earthquake,6.2,3.2,0.083,14,reviewed,us,us
2022-01-19T14:29:40.403Z,37.3051,-116.0623,3,0.5,ml,10,290.17,0.085,0.1494,nn,nn00831960,2022-01-20T02:36:40.858Z,"47 km SW of Rachel, Nevada",earthquake,,4.1,0.76,5,reviewed,nn,nn
2022-01-19T14:24:38.921Z,56.3594,-148.7055,10,3.7,ml,,247,2.553,0.49,us,us7000gd5e,2022-01-21T16:00:46.040Z,"258 km SE of Chiniak, Alaska",earthquake,2.5,2,0.048,58,reviewed,us,us
2022-01-19T14:20:01.860Z,38.8416672,-122.8274994,2.66,0.37,md,10,78,0.006954,0.02,nc,nc73680621,2022-01-19T14:21:38.851Z,"9km WNW of Cobb, CA",earthquake,0.72,1.8,,1,automatic,nc,nc
2022-01-19T14:18:45.930Z,19.4951666666667,-155.6535,-0.19,2.28,ml,51,60,,0.16,hv,hv72881362,2022-01-19T21:06:04.640Z,"22 km E of Honaunau-Napoopoo, Hawaii",earthquake,0.2,0.46,0.179718579925521,12,reviewed,hv,hv
2022-01-19T14:14:40.590Z,44.8216667,-110.765,8.07,-0.51,md,5,281,0.0694,0.01,uu,uu60029849,2022-01-19T16:52:24.030Z,"17 km SSW of Mammoth, Wyoming",earthquake,2.56,0.96,0.33,3,reviewed,uu,uu
2022-01-19T14:14:26.490Z,44.8206667,-110.7861667,8.44,0.59,md,10,237,0.05606,0.06,uu,uu60478072,2022-01-19T16:49:47.130Z,"18 km SSW of Mammoth, Wyoming",earthquake,1.54,0.68,0.496,5,reviewed,uu,uu
2022-01-19T14:13:28.107Z,64.5523,-146.9634,0.1,0.9,ml,,,,1.03,ak,ak022vnmibo,2022-01-19T14:22:42.568Z,"4 km NW of Salcha, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-19T14:06:26.270Z,38.8264999,-122.8021698,2.81,0.35,md,10,101,0.006909,0.01,nc,nc73680616,2022-01-19T14:08:03.865Z,"7km NW of The Geysers, CA",earthquake,0.38,1.07,,1,automatic,nc,nc
2022-01-19T13:56:00.020Z,37.5815,-118.9863333,5.79,0.11,md,11,131,0.0418,0.05,nc,nc73680611,2022-01-19T16:18:54.037Z,"6km S of Mammoth Lakes, CA",earthquake,0.52,1,0.307,10,reviewed,nc,nc
2022-01-19T13:55:22.200Z,54.5658333333333,-163.304833333333,13.76,1.6,ml,8,210,,0.13,av,av91467051,2022-01-21T07:00:36.000Z,"32 km SSE of False Pass, Alaska",earthquake,1.25,1.38,0.214368485677186,10,reviewed,av,av
2022-01-19T13:44:37.850Z,62.592,-149.172,53.5,1.5,ml,,,,0.86,ak,ak022vn7qo9,2022-01-19T13:47:28.920Z,"50 km ENE of Chase, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-19T13:43:45.730Z,38.8336678,-122.8171692,1.33,0.89,md,20,58,0.01166,0.03,nc,nc73680596,2022-01-19T13:45:23.149Z,"8km NW of The Geysers, CA",earthquake,0.22,0.51,0.13,4,automatic,nc,nc
2022-01-19T13:17:53.289Z,36.537,-98.9545,7.18,1.28,ml,19,89,0.04409134777,0.15,ok,ok2022bhxj,2022-01-20T13:51:31.426Z,"8 km SW of Waynoka, Oklahoma",earthquake,,0.4,0.15,8,reviewed,ok,ok
2022-01-19T13:10:58.040Z,38.7886667,-122.7238333,1.65,0.62,md,29,50,0.006761,0.03,nc,nc73680576,2022-01-19T18:09:01.910Z,"3km ENE of The Geysers, CA",earthquake,0.15,0.3,0.146,6,reviewed,nc,nc
2022-01-19T13:05:30.786Z,38.1703,-117.9634,2.5,0.8,ml,12,144.75,0.032,0.1084,nn,nn00831931,2022-01-19T18:16:12.761Z,"27 km SSE of Mina, Nevada",earthquake,,1,0.61,4,reviewed,nn,nn
2022-01-19T13:05:03.983Z,36.7307,-115.9208,2.8,0.2,ml,9,263.37,0.052,0.1642,nn,nn00831959,2022-01-20T02:36:39.733Z,"28 km NW of Indian Springs, Nevada",earthquake,,2.3,0.12,2,reviewed,nn,nn
2022-01-19T13:04:28.010Z,36.0055,-117.7893333,1.84,0.2,ml,9,115,0.02771,0.04,ci,ci39916599,2022-01-19T16:31:02.116Z,"13km NE of Little Lake, CA",earthquake,0.14,0.15,0.244,3,reviewed,ci,ci
2022-01-19T13:01:19.050Z,33.7315,-116.8933333,4.41,0.38,ml,11,142,0.09314,0.08,ci,ci39916591,2022-01-19T16:27:09.927Z,"2km S of Valle Vista, CA",earthquake,0.2,0.51,0.099,2,reviewed,ci,ci
2022-01-19T12:55:47.896Z,38.168,-117.8896,7.6,2,ml,19,87.18,0.062,0.1263,nn,nn00831928,2022-01-19T17:04:32.494Z,"31 km SE of Mina, Nevada",earthquake,,1.3,0.17,7,reviewed,nn,nn
2022-01-19T12:53:58.990Z,37.599,-118.9853333,5.5,0.47,md,15,121,0.03171,0.05,nc,nc73680566,2022-01-19T16:13:24.169Z,"4km S of Mammoth Lakes, CA",earthquake,0.48,0.63,0.125,13,reviewed,nc,nc
2022-01-19T12:52:43.770Z,19.2145004272461,-155.392166137695,32.2000007629395,1.85000002,md,44,155,,0.119999997,hv,hv72881272,2022-01-19T12:58:13.640Z,"9 km E of Pāhala, Hawaii",earthquake,0.55,0.819999993,0.550000012,13,automatic,hv,hv
2022-01-19T12:28:50.310Z,19.2066669464111,-155.429504394531,33.6399993896484,2.00999999,md,44,143,,0.109999999,hv,hv72881247,2022-01-19T12:32:05.800Z,"Island of Hawaii, Hawaii",earthquake,0.49,0.720000029,1.67999995,10,automatic,hv,hv
2022-01-19T12:28:12.460Z,62.7438,-151.0035,90.6,1.6,ml,,,,0.46,ak,ak022vmitnj,2022-01-19T12:40:12.247Z,"30 km NNW of Petersville, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-19T12:23:17.390Z,33.7116667,-116.8076667,15.72,0.63,ml,23,156,0.07794,0.12,ci,ci39916559,2022-01-19T17:41:19.829Z,"9km WSW of Idyllwild, CA",earthquake,0.35,0.44,0.061,8,reviewed,ci,ci
2022-01-19T11:57:54.250Z,17.9286,-66.9138,13,2.07,md,6,254,0.058,0.16,pr,pr2022019007,2022-01-19T12:25:51.120Z,"4 km S of Guánica, Puerto Rico",earthquake,1.16,0.8,0.14,3,reviewed,pr,pr
2022-01-19T11:51:53.520Z,33.7315,-116.0391667,5.11,0.59,ml,17,163,0.08668,0.12,ci,ci39916551,2022-01-19T16:42:33.946Z,"14km ENE of Coachella, CA",earthquake,0.28,1.03,0.038,6,reviewed,ci,ci
2022-01-19T11:48:41.404Z,62.9279,-150.8784,57.1,1.5,ml,,,,1.61,ak,ak022vm1qlo,2022-01-19T11:52:37.255Z,"48 km N of Petersville, Alaska",earthquake,,1.2,,,automatic,ak,ak
2022-01-19T11:45:15.340Z,33.7363333,-116.8931667,3.83,0.55,ml,20,134,0.09459,0.09,ci,ci39916543,2022-01-19T17:27:43.511Z,"1km S of Valle Vista, CA",earthquake,0.18,0.39,0.166,9,reviewed,ci,ci
2022-01-19T11:45:08.730Z,33.7341667,-116.8918333,3.9,0.2,ml,16,138,0.09504,0.07,ci,ci37379804,2022-01-19T17:32:51.790Z,"2km S of Valle Vista, CA",earthquake,0.18,0.39,0.142,5,reviewed,ci,ci
2022-01-19T11:43:10.990Z,33.7381667,-116.9548333,13.52,0.55,ml,26,92,0.04912,0.14,ci,ci39916535,2022-01-19T17:20:21.954Z,"2km ESE of Hemet, CA",earthquake,0.24,0.44,0.23,12,reviewed,ci,ci
2022-01-19T11:42:57.880Z,44.9698333,-113.0135,8.37,1.06,ml,8,132,0.184,0.19,mb,mb80536369,2022-01-20T16:23:25.410Z,"40 km SW of Dillon, Montana",earthquake,0.92,3.49,0.139,6,reviewed,mb,mb
2022-01-19T11:41:05.540Z,38.8411674,-122.8263321,1.19,0.86,md,14,102,0.007599,0.03,nc,nc73680551,2022-01-19T11:42:43.461Z,"9km WNW of Cobb, CA",earthquake,0.25,0.53,,1,automatic,nc,nc
2022-01-19T11:40:12.980Z,33.7056667,-116.7451667,15.79,0.49,ml,19,71,0.02642,0.06,ci,ci39916527,2022-01-19T15:09:45.062Z,"4km SSW of Idyllwild, CA",earthquake,0.17,0.26,0.293,6,reviewed,ci,ci
2022-01-19T11:37:50.073Z,-20.564,-175.3449,10,4.6,mb,,83,6.762,0.44,us,us7000gdqy,2022-01-21T21:23:55.040Z,"65 km NNW of Nuku‘alofa, Tonga",earthquake,11.4,1.8,0.102,37,reviewed,us,us
2022-01-19T11:31:17.860Z,46.234,-122.633166666667,15.05,0.52,ml,9,106,0.1992,0.13,uw,uw61802717,2022-01-20T03:43:07.430Z,"21 km ESE of Castle Rock, Washington",earthquake,0.39,1.45,0.0567916737269245,6,reviewed,uw,uw
2022-01-19T11:28:15.300Z,34.0986667,-116.4028333,7.12,0.95,ml,25,139,0.1577,0.14,ci,ci39916519,2022-01-19T17:13:59.925Z,"3km ESE of Yucca Valley, CA",earthquake,0.21,0.7,0.144,9,reviewed,ci,ci
2022-01-19T10:56:39.950Z,33.7356667,-116.8973333,2.92,1.01,ml,50,59,0.09108,0.16,ci,ci39916511,2022-01-19T16:58:15.454Z,"1km SSW of Valle Vista, CA",earthquake,0.13,0.47,0.202,25,reviewed,ci,ci
2022-01-19T10:51:04.613Z,62.9719,-150.3047,83.6,1.4,ml,,,,0.41,ak,ak022vlgvb9,2022-01-19T10:55:21.382Z,"58 km NNE of Petersville, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-19T10:50:20.220Z,35.1498333,-118.1931667,7.4,1.17,ml,26,69,0.1448,0.17,ci,ci39916503,2022-01-19T14:30:34.038Z,"11km N of Mojave, CA",earthquake,0.31,1.86,0.122,22,reviewed,ci,ci
2022-01-19T10:46:18.040Z,32.9131667,-116.2883333,7.98,0.78,ml,24,90,0.2013,0.18,ci,ci39916495,2022-01-19T17:21:14.097Z,"25km ENE of Pine Valley, CA",earthquake,0.26,2.15,0.1,7,reviewed,ci,ci
2022-01-19T10:45:12.200Z,46.8986667,-112.5186667,14.25,0.98,ml,11,96,0.058,0.12,mb,mb80536364,2022-01-19T15:35:50.120Z,"Western Montana",earthquake,0.53,0.54,0.215,4,reviewed,mb,mb
2022-01-19T10:43:22.014Z,36.8436,-116.2334,3.5,-0.3,ml,5,111.99,0.062,0.1064,nn,nn00831958,2022-01-20T02:36:38.500Z,"47 km E of Beatty, Nevada",earthquake,,9.3,0.29,4,reviewed,nn,nn
2022-01-19T10:36:51.401Z,38.9719,-118.743,4.1,1.1,ml,17,114.8,0.387,0.1729,nn,nn00831926,2022-01-19T17:54:29.257Z,"6 km ENE of Schurz, Nevada",earthquake,,2.2,0.47,6,reviewed,nn,nn
2022-01-19T10:31:57.600Z,33.7343333,-116.894,3.02,0.59,ml,27,74,0.09335,0.15,ci,ci39916479,2022-01-19T17:14:13.085Z,"2km S of Valle Vista, CA",earthquake,0.2,0.67,0.141,8,reviewed,ci,ci
2022-01-19T10:30:39.400Z,38.8063316,-122.8174973,3.2,0.35,md,7,139,0.009471,0.01,nc,nc73680541,2022-01-19T10:32:17.502Z,"6km WNW of The Geysers, CA",earthquake,1.4,1.43,,1,automatic,nc,nc
2022-01-19T10:26:40.285Z,38.1641,-117.9002,10.3,1.7,ml,20,109.29,0.053,0.1313,nn,nn00831922,2022-01-19T17:13:58.462Z,"31 km SE of Mina, Nevada",earthquake,,0.9,0.08,8,reviewed,nn,nn
2022-01-19T10:21:03.430Z,38.4851667,-112.8415,1.78,0.02,md,8,105,0.02609,0.06,uu,uu60478067,2022-01-19T16:44:05.170Z,"17 km ENE of Milford, Utah",earthquake,0.36,0.92,0.272,3,reviewed,uu,uu
2022-01-19T10:18:05.320Z,44.825,-110.7608333,8.19,0.21,md,9,243,0.07361,0.06,uu,uu60478062,2022-01-19T16:30:11.460Z,"17 km SSW of Mammoth, Wyoming",earthquake,1.74,0.94,0.426,6,reviewed,uu,uu
2022-01-19T10:15:43.217Z,38.5209,-119.5048,7.7,0.7,ml,5,139.68,0.066,0.0906,nn,nn00831998,2022-01-20T02:36:55.889Z,"2 km WNW of Walker, California",earthquake,,2.1,0.07,2,reviewed,nn,nn
2022-01-19T10:14:54.410Z,38.840332,-122.7454987,0.5,1.15,md,13,170,0.02146,0.05,nc,nc73680536,2022-01-19T10:47:12.671Z,"3km NW of Cobb, CA",earthquake,0.42,0.72,0.04,2,automatic,nc,nc
2022-01-19T10:10:55.350Z,38.7906685,-122.7678299,1.25,0.21,md,12,91,0.01179,0.03,nc,nc73680531,2022-01-19T10:12:31.825Z,"2km NNW of The Geysers, CA",earthquake,0.31,0.71,0.15,2,automatic,nc,nc
2022-01-19T10:10:51.720Z,44.9756667,-113.0225,6.24,1.01,ml,8,176,0.193,0.2,mb,mb80536384,2022-01-19T16:52:24.760Z,"40 km SW of Dillon, Montana",earthquake,0.92,4,0.159,6,reviewed,mb,mb
2022-01-19T10:01:56.720Z,46.2405,-122.630333333333,15.67,0.99,ml,20,54,0.1986,0.18,uw,uw61802712,2022-01-20T02:12:15.450Z,"21 km E of Castle Rock, Washington",earthquake,0.35,1.38,0.100156818520219,9,reviewed,uw,uw
2022-01-19T09:59:13.750Z,38.3076667,-122.6288333,5.54,1.16,md,26,55,0.05733,0.11,nc,nc73680526,2022-01-19T13:11:11.525Z,"3km ENE of Penngrove, CA",earthquake,0.24,0.57,0.146,20,reviewed,nc,nc
2022-01-19T09:52:15.957Z,61.8127,-150.6194,65.8,1.2,ml,,,,0.45,ak,ak022vkvn39,2022-01-19T17:43:34.487Z,"30 km N of Susitna, Alaska",earthquake,,0.5,,,reviewed,ak,ak
2022-01-19T09:47:20.130Z,19.2059993743896,-155.41650390625,31.8299999237061,1.83000004,md,38,148,,0.150000006,hv,hv72881142,2022-01-19T09:50:39.020Z,"6 km E of Pāhala, Hawaii",earthquake,0.58,0.720000029,1.62,6,automatic,hv,hv
2022-01-19T09:31:47.574Z,63.0695,-151.5476,0,1.5,ml,,,,1.19,ak,ak022vkr8hs,2022-01-19T09:40:53.757Z,"53 km S of Denali National Park, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-19T09:29:00.889Z,37.4812,-114.5833,4.9,0.6,ml,3,158.62,0.472,0.0983,nn,nn00831957,2022-01-20T02:36:37.784Z,"16 km SSW of Caliente, Nevada",earthquake,,13.2,0,1,reviewed,nn,nn
2022-01-19T09:19:18.822Z,36.6504,-116.2774,6.9,0.1,ml,9,191.83,0.05,0.0932,nn,nn00831956,2022-01-20T02:36:36.344Z,"51 km SE of Beatty, Nevada",earthquake,,1.9,0.15,3,reviewed,nn,nn
2022-01-19T09:10:45.105Z,38.5656,-119.4902,5.7,1.1,ml,11,141.49,0.031,0.1376,nn,nn00831971,2022-01-20T02:36:53.224Z,"1 km E of Coleville, California",earthquake,,1.5,0.24,3,reviewed,nn,nn
2022-01-19T09:03:56.790Z,54.1468333333333,-165.9675,2.11,-0.96,ml,5,114,,0.25,av,av91047438,2022-01-21T06:27:16.940Z,"12 km W of Akutan, Alaska",earthquake,0.56,1.32,0.154278116130945,4,reviewed,av,av
2022-01-19T08:54:11.495Z,63.5817,-147.2843,0,1.8,ml,,,,0.89,ak,ak022vkanpw,2022-01-19T08:58:29.404Z,"82 km ESE of Denali Park, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-19T08:47:01.215Z,63.128,-150.8828,119.8,1.6,ml,,,,0.18,ak,ak022vk94yx,2022-01-19T08:50:08.288Z,"62 km SE of Denali National Park, Alaska",earthquake,,2.5,,,automatic,ak,ak
2022-01-19T08:45:45.907Z,31.66604235,-104.3587613,7.596923828000001,2.4,ml,33,60,0.08021325005,0.3,tx,tx2022bhok,2022-01-21T23:04:50.369Z,"56 km S of Whites City, New Mexico",earthquake,1.134741552,0.9741269098,0.2,15,reviewed,tx,tx
2022-01-19T08:37:24.940Z,33.7328333,-116.8956667,4.3,0.61,ml,35,58,0.09161,0.11,ci,ci39916471,2022-01-19T16:58:24.070Z,"2km S of Valle Vista, CA",earthquake,0.14,0.3,0.15,14,reviewed,ci,ci
2022-01-19T08:33:09.331Z,63.2576,-150.4907,127.4,1.6,ml,,,,0.18,ak,ak022vk65kl,2022-01-19T08:38:57.103Z,"69 km ESE of Denali National Park, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-19T08:19:23.349Z,63.094,-150.4117,88.1,1.6,ml,,,,0.49,ak,ak022vk36my,2022-01-19T08:24:15.495Z,"69 km NNE of Petersville, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-19T08:18:57.700Z,19.3053,-68.7691,60,3.98,md,17,337,0.8813,0.41,pr,pr2022019006,2022-01-20T07:18:06.040Z,"46 km NE of Miches, Dominican Republic",earthquake,4.89,19.51,0.11,12,reviewed,pr,pr
2022-01-19T08:05:12.426Z,59.5852,-138.889,0.2,3,ml,,,,0.72,ak,ak022vk05rz,2022-01-20T06:54:29.040Z,"47 km E of Yakutat, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-19T07:57:21.060Z,19.2181663513184,-155.419494628906,34.3600006103516,1.86000001,md,40,137,,0.109999999,hv,hv72881047,2022-01-19T08:01:44.910Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.56,0.779999971,0.920000017,11,automatic,hv,hv
2022-01-19T07:54:50.888Z,61.355,-140.9834,11.6,1.3,ml,,,,0.16,ak,ak022vjpb8c,2022-01-19T07:58:32.442Z,"103 km E of McCarthy, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-19T07:50:40.433Z,61.3542,-141.047,0,2,ml,,,,0.73,ak,ak022vjofja,2022-01-19T07:56:52.120Z,"100 km E of McCarthy, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-19T07:48:56.979Z,-20.5827,-175.3163,10,4.8,mb,,170,6.873,0.56,us,us7000gdp8,2022-01-20T23:07:45.040Z,"62 km N of Nuku‘alofa, Tonga",earthquake,6.5,1.9,0.085,47,reviewed,us,us
2022-01-19T07:48:18.700Z,33.7368333,-116.895,2.64,0.55,ml,22,122,0.09329,0.15,ci,ci39916463,2022-01-19T16:51:14.917Z,"1km S of Valle Vista, CA",earthquake,0.23,0.35,0.155,9,reviewed,ci,ci
2022-01-19T07:47:57.510Z,19.574333190918,-155.700668334961,6.69999980926514,1.70000005,md,36,96,,0.230000004,hv,hv72881042,2022-01-19T07:53:27.280Z,"21 km NE of Honaunau-Napoopoo, Hawaii",earthquake,0.53,0.589999974,1.26999998,7,automatic,hv,hv
2022-01-19T07:47:31.810Z,17.9256,-66.693,17,2.46,md,11,240,0.1458,0.1,pr,pr2022019005,2022-01-19T14:01:47.704Z,"8 km SSE of Tallaboa, Puerto Rico",earthquake,0.56,0.46,0.16,5,reviewed,pr,pr
2022-01-19T07:43:12.560Z,38.8268318,-122.8516693,1.38,1.29,md,22,61,0.01352,0.04,nc,nc73680516,2022-01-19T08:15:11.799Z,"10km WNW of The Geysers, CA",earthquake,0.19,0.5,0.12,4,automatic,nc,nc
2022-01-19T07:43:01.027Z,38.1123,-118.4366,1.5,0,ml,6,318.51,0.149,0.0675,nn,nn00831969,2022-01-20T02:36:51.015Z,"32 km N of Benton, California",earthquake,,6.6,0,1,reviewed,nn,nn
2022-01-19T07:31:45.881Z,64.0871,-148.2344,105.6,1.5,ml,,,,0.42,ak,ak022vjkdcs,2022-01-19T07:34:39.505Z,"43 km E of Ferry, Alaska",earthquake,,1.9,,,automatic,ak,ak
2022-01-19T07:22:22.860Z,44.7946667,-110.8153333,6.53,0.69,md,10,234,0.02583,0.08,uu,uu60478052,2022-01-19T16:23:28.700Z,"22 km SSW of Mammoth, Wyoming",earthquake,1.11,1.09,0.35,6,reviewed,uu,uu
2022-01-19T07:21:02.230Z,33.9908333,-116.9776667,4.46,0.86,ml,38,113,0.06583,0.13,ci,ci39916455,2022-01-19T16:44:30.860Z,"7km N of Beaumont, CA",earthquake,0.18,0.31,0.102,13,reviewed,ci,ci
2022-01-19T07:17:34.780Z,54.1425,-165.972166666667,2.16,-0.61,ml,7,88,,0.13,av,av91047433,2022-01-21T04:36:26.750Z,"12 km W of Akutan, Alaska",earthquake,0.2,0.44,0.164117085266025,6,reviewed,av,av
2022-01-19T07:13:21.086Z,36.7491,-116.2814,0.1,0,ml,4,318.94,0.059,0.0444,nn,nn00831955,2022-01-19T19:46:08.208Z,"46 km ESE of Beatty, Nevada",earthquake,,19.2,0,1,reviewed,nn,nn
2022-01-19T07:12:28.330Z,19.1525,-155.466333333333,31.76,1.55,md,23,168,,0.11,hv,hv72881017,2022-01-19T22:27:05.390Z,"Island of Hawaii, Hawaii",earthquake,0.62,0.7,0.126073427764491,15,reviewed,hv,hv
2022-01-19T07:03:39.800Z,17.9145,-66.852,16,2.47,md,14,218,0.0664,0.1,pr,pr2022019004,2022-01-19T07:16:45.141Z,"8 km SSE of Maria Antonia, Puerto Rico",earthquake,0.58,0.7,0.22,9,reviewed,pr,pr
2022-01-19T07:03:17.790Z,38.8348351,-122.8183365,1.73,0.85,md,7,136,0.01312,0.01,nc,nc73680506,2022-01-19T07:04:52.807Z,"8km NW of The Geysers, CA",earthquake,0.64,1.84,,1,automatic,nc,nc
2022-01-19T07:01:31.886Z,61.7255,-147.8937,38.6,0.9,ml,,,,0.16,ak,ak022vjdwsk,2022-01-19T07:05:56.561Z,"15 km SW of Glacier View, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-19T07:00:26.710Z,38.8216667,-122.7916641,1.79,0.35,md,7,86,0.012,0.01,nc,nc73680501,2022-01-19T07:02:02.424Z,"6km NNW of The Geysers, CA",earthquake,0.51,1.84,,1,automatic,nc,nc
2022-01-19T07:00:04.590Z,38.7713333,-122.716,1.49,-0.18,md,12,52,0.01143,0.04,nc,nc73680496,2022-01-21T00:33:08.468Z,"2km W of Anderson Springs, CA",earthquake,0.29,0.29,,1,reviewed,nc,nc
2022-01-19T06:28:27.186Z,61.3374,-150.3012,45.2,1.3,ml,,,,0.52,ak,ak022viy95q,2022-01-19T06:31:33.085Z,"17 km W of Point MacKenzie, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-19T06:23:57.374Z,36.6969,67.9853,10,4.2,mb,,109,2.12,1.34,us,us7000gd3v,2022-01-20T06:22:18.040Z,"25 km E of Khulm, Afghanistan",earthquake,4.9,1.9,0.186,9,reviewed,us,us
2022-01-19T06:09:51.370Z,43.7985,-110.3256667,11.19,1.32,ml,11,221,0.274,0.18,mb,mb80536359,2022-01-19T15:16:43.940Z,"30 km NE of Kelly, Wyoming",earthquake,1.48,1.07,0.345,7,reviewed,mb,mb
2022-01-19T06:05:37.707Z,30.5084,50.6501,10,4.6,mb,,82,6.191,1.05,us,us7000gd3t,2022-01-19T07:36:32.040Z,"21 km NW of Dogonbadan, Iran",earthquake,9,1.9,0.076,52,reviewed,us,us
2022-01-19T06:05:08.780Z,37.618,-118.8008333,4.7,0.29,md,11,229,0.03422,0.05,nc,nc73680481,2022-01-19T07:39:41.576Z,"12km WNW of Toms Place, CA",earthquake,0.67,1,0.29,13,reviewed,nc,nc
2022-01-19T06:03:35.590Z,39.4238333,-110.3036667,-2.36,2.04,ml,11,197,0.0166,0.15,uu,uu60478042,2022-01-19T14:13:56.620Z,"15 km SSE of Sunnyside, Utah",earthquake,0.85,2.24,0.073,2,reviewed,uu,uu
2022-01-19T06:03:02.948Z,38.0786,-118.7605,15.5,1.2,ml,11,128.12,0.265,0.1305,nn,nn00831967,2022-01-20T02:36:50.323Z,"33 km E of Mono City, California",earthquake,,5.7,0.12,3,reviewed,nn,nn
2022-01-19T05:46:11.629Z,-52.5133,12.9174,10,5.4,mb,,90,20.455,0.51,us,us7000gd3p,2022-01-20T05:49:46.036Z,"southwest of Africa",earthquake,9.2,1.9,0.069,72,reviewed,us,us
2022-01-19T05:35:52.210Z,33.6631667,-116.7165,16.13,0.62,ml,23,60,0.04792,0.18,ci,ci39916415,2022-01-19T14:31:45.686Z,"8km S of Idyllwild, CA",earthquake,0.44,0.59,0.192,10,reviewed,ci,ci
2022-01-19T05:34:39.586Z,-20.6282,-175.6985,10,4.6,mb,,129,6.564,1.12,us,us7000gdzh,2022-01-21T20:10:22.040Z,"Tonga",earthquake,9.6,1.9,0.075,53,reviewed,us,us
2022-01-19T05:34:05.860Z,39.4178333,-110.3016667,-2.35,1.7,md,7,199,0.0192,0.12,uu,uu60478032,2022-01-19T16:17:43.990Z,"16 km SSE of Sunnyside, Utah",earthquake,0.98,2.32,0.327,5,reviewed,uu,uu
2022-01-19T05:33:43.500Z,35.6355,-85.6551667,13.83,2.32,md,13,87,0.4757,0.07,se,se60143143,2022-01-20T10:34:01.019Z,"11 km ESE of McMinnville, Tennessee",earthquake,0.79,1.64,0.129,13,reviewed,se,se
2022-01-19T05:31:19.610Z,33.6473333,-116.7126667,13.68,0.29,ml,15,91,0.06368,0.11,ci,ci39916407,2022-01-19T14:31:59.687Z,"10km S of Idyllwild, CA",earthquake,0.37,0.55,0.18,5,reviewed,ci,ci
2022-01-19T05:20:49.110Z,46.6936666666667,-121.077666666667,12.78,0.81,ml,16,138,0.1784,0.14,uw,uw61802697,2022-01-20T04:27:37.410Z,"17 km SW of Nile, Washington",earthquake,0.45,2.16,0.130681667686589,9,reviewed,uw,uw
2022-01-19T05:14:50.770Z,35.6473333,-117.4273333,2.62,0.42,ml,15,169,0.06702,0.15,ci,ci39916399,2022-01-19T16:31:04.199Z,"14km S of Searles Valley, CA",earthquake,0.42,0.42,0.037,5,reviewed,ci,ci
2022-01-19T05:06:17.510Z,38.8406677,-122.838501,2.03,0.86,md,11,120,0.003138,0.01,nc,nc73680471,2022-01-19T05:07:51.703Z,"10km NW of The Geysers, CA",earthquake,0.33,0.64,,1,automatic,nc,nc
2022-01-19T04:56:01.219Z,36.6781,-116.2166,2.6,0.1,ml,4,179.72,0.033,0.1944,nn,nn00831953,2022-01-19T19:24:28.244Z,"50 km WNW of Indian Springs, Nevada",earthquake,,4.9,0,1,reviewed,nn,nn
2022-01-19T04:52:22.200Z,33.9558333,-118.3718333,12.05,1.6,ml,45,62,0.03562,0.22,ci,ci39916391,2022-01-19T16:28:05.580Z,"2km W of Inglewood, CA",earthquake,0.24,0.36,0.192,40,reviewed,ci,ci
2022-01-19T04:50:33.620Z,38.8260002,-122.8528366,3.01,0.86,md,9,102,0.00351,0.02,nc,nc73680466,2022-01-19T04:52:11.409Z,"10km WNW of The Geysers, CA",earthquake,0.53,1.31,,1,automatic,nc,nc
2022-01-19T04:50:12.470Z,38.8261681,-122.8544998,2.61,0.86,md,12,93,0.002308,0.02,nc,nc73680461,2022-01-19T04:51:47.386Z,"10km WNW of The Geysers, CA",earthquake,0.32,0.58,0.01,2,automatic,nc,nc
2022-01-19T04:43:59.260Z,46.6926666666667,-121.079166666667,13.86,0.65,ml,13,138,0.1796,0.11,uw,uw61802692,2022-01-20T04:42:30.780Z,"17 km SW of Nile, Washington",earthquake,0.48,1.62,0.162639823828956,6,reviewed,uw,uw
2022-01-19T04:42:10.487Z,61.3564,-140.0738,0,1.4,ml,,,,0.77,ak,ak022vhucon,2022-01-19T04:47:32.819Z,"152 km E of McCarthy, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-19T04:40:38.073Z,61.394,-140.0579,10.8,1.6,ml,,,,0.56,ak,ak022vhtzdt,2022-01-19T04:45:52.534Z,"152 km E of McCarthy, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-19T04:38:47.460Z,19.1326,-66.8513,18,3.29,md,18,230,0.7141,0.46,pr,pr2022019003,2022-01-19T05:01:09.629Z,"71 km N of Hatillo, Puerto Rico",earthquake,1.9,5.13,0.05,8,reviewed,pr,pr
2022-01-19T04:34:47.724Z,63.6168,-147.069,9.4,1.3,ml,,,,0.8,ak,ak022vhspty,2022-01-19T04:39:01.638Z,"80 km SW of Delta Junction, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-19T04:30:30.100Z,36.6469,-116.2777,7.3,-0.1,ml,8,197.06,0.049,0.1259,nn,nn00831952,2022-01-19T19:21:20.910Z,"51 km SE of Beatty, Nevada",earthquake,,2.3,0.14,3,reviewed,nn,nn
2022-01-19T04:25:47.843Z,5.4009,-72.5531,10,4.6,mb,,50,0.719,0.39,us,us7000gd37,2022-01-21T04:06:01.557Z,"Colombia",earthquake,5.1,1.9,0.06,82,reviewed,us,us
2022-01-19T04:25:07.150Z,40.7321667,-112.0496667,4.74,0.63,md,18,44,0.0117,0.14,uu,uu60478027,2022-01-19T15:03:11.930Z,"5 km ENE of Magna, Utah",earthquake,0.29,0.51,0.149,8,reviewed,uu,uu
2022-01-19T04:03:10.160Z,39.4168333,-110.2903333,-3.37,1.71,md,7,202,0.02789,0.12,uu,uu60478022,2022-01-19T16:18:08.680Z,"17 km SSE of Sunnyside, Utah",earthquake,1.54,3.3,0.181,7,reviewed,uu,uu
2022-01-19T03:54:20.430Z,33.8336667,-118.2693333,10.63,1.14,ml,18,73,0.03432,0.27,ci,ci39916359,2022-01-19T16:10:57.659Z,"1km ENE of Carson, CA",earthquake,0.6,0.71,0.129,16,reviewed,ci,ci
2022-01-19T03:48:36.510Z,33.7358333,-116.8935,2.35,1.12,ml,34,46,0.09418,0.15,ci,ci39916351,2022-01-19T14:32:25.842Z,"1km S of Valle Vista, CA",earthquake,0.17,0.32,0.223,28,reviewed,ci,ci
2022-01-19T03:41:55.550Z,19.1889991760254,-155.471832275391,33.2299995422363,1.79999995,md,42,91,,0.100000001,hv,hv72880872,2022-01-19T03:45:15.670Z,"1 km SSE of Pāhala, Hawaii",earthquake,0.49,0.829999983,1.89999998,4,automatic,hv,hv
2022-01-19T03:37:40.720Z,19.0538330078125,-155.345672607422,33.2799987792969,2.14,ml,50,212,,0.119999997,hv,hv72880867,2022-01-21T02:52:48.040Z,"21 km SE of Pāhala, Hawaii",earthquake,0.66,1,4.11,8,automatic,hv,hv
2022-01-19T03:37:29.686Z,-20.4401,-175.3146,10,4.6,mb,,86,6.82,0.66,us,us7000gdf7,2022-01-20T22:35:34.040Z,"78 km N of Nuku‘alofa, Tonga",earthquake,13.2,1.9,0.077,58,reviewed,us,us
2022-01-19T03:26:30.300Z,51.8148333333333,-177.770333333333,7.01,1.34,ml,8,137,,0.11,av,av91466561,2022-01-21T03:10:12.250Z,"78 km W of Adak, Alaska",earthquake,0.45,0.43,0.242903863046734,8,reviewed,av,av
2022-01-19T03:25:22.670Z,33.7333333,-116.8915,1.5,0.64,ml,19,59,0.09509,0.15,ci,ci39916327,2022-01-19T14:32:58.771Z,"2km S of Valle Vista, CA",earthquake,0.23,0.34,0.215,15,reviewed,ci,ci
2022-01-19T03:25:07.120Z,46.7378333333333,-121.553666666667,5.41,1.1,ml,21,111,0.1358,0.14,uw,uw61802687,2022-01-20T02:19:52.280Z,"17 km NNE of Packwood, Washington",earthquake,0.34,0.56,0.167655805454384,10,reviewed,uw,uw
2022-01-19T03:21:47.352Z,38.2122,-117.7279,5.3,1.3,ml,17,128,0.137,0.13,nn,nn00831920,2022-01-19T17:41:57.371Z,"38 km ESE of Mina, Nevada",earthquake,,3,0.16,8,reviewed,nn,nn
2022-01-19T03:16:04.030Z,51.9295,-176.557166666667,2.46,1.91,ml,13,123,,0.27,av,av91466551,2022-01-21T02:44:00.920Z,"Andreanof Islands, Aleutian Islands, Alaska",earthquake,0.62,0.85,0.311276968387514,13,reviewed,av,av
2022-01-19T03:05:06.380Z,18.0678,-68.3258,69,3.63,md,25,193,0.4495,0.37,pr,pr2022019002,2022-01-21T03:43:12.040Z,"45 km SE of Boca de Yuma, Dominican Republic",earthquake,1.22,1.5,0.14,18,reviewed,pr,pr
2022-01-19T02:59:48.368Z,10.9914,-62.3114,105.21,4.8,mb,,69,1.304,1.01,us,us7000gd2r,2022-01-19T15:00:41.269Z,"45 km N of Güiria, Venezuela",earthquake,9.1,7.9,0.037,232,reviewed,us,us
2022-01-19T02:49:30.522Z,39.2484,-120.1164,9,0.4,ml,6,112.93,0.042,0.0958,nn,nn00831966,2022-01-20T02:36:48.763Z,"3 km NW of Carnelian Bay, California",earthquake,,1.8,0.25,4,reviewed,nn,nn
2022-01-19T02:41:50.618Z,40.078,-119.67,14,-0.2,ml,3,176.45,0.104,0.0223,nn,nn00831965,2022-01-20T02:36:45.018Z,"15 km NNW of Sutcliffe, Nevada",earthquake,,6,0.11,2,reviewed,nn,nn
2022-01-19T02:39:55.876Z,36.7333,-116.2483,6.6,-0.4,ml,7,208.37,0.029,0.0625,nn,nn00831951,2022-01-19T19:15:07.420Z,"49 km ESE of Beatty, Nevada",earthquake,,1.9,0.15,5,reviewed,nn,nn
2022-01-19T02:30:08.986Z,31.67129565,-104.3639203,7.365551758,2.9,ml,38,58,0.08441606252,0.2,tx,tx2022bhca,2022-01-21T00:54:56.046Z,"55 km S of Whites City, New Mexico",earthquake,0.7767378575,0.8768919743,0.1,18,reviewed,tx,tx
2022-01-19T02:10:06.045Z,-20.8442,-175.3193,10,4.6,mb,,118,6.977,0.69,us,us7000gdza,2022-01-22T01:03:15.040Z,"34 km NNW of Nuku‘alofa, Tonga",earthquake,10.3,1.9,0.084,44,reviewed,us,us
2022-01-19T02:00:59.288Z,36.7253,-116.1809,6,-0.5,ml,7,144.04,0.026,0.0825,nn,nn00831950,2022-01-19T19:08:54.494Z,"48 km WNW of Indian Springs, Nevada",earthquake,,1.8,0.21,4,reviewed,nn,nn
2022-01-19T01:56:36.274Z,60.7379,-43.9572,10,4.6,mb,,70,0.829,1.02,us,us7000gd2f,2022-01-19T02:23:59.040Z,"96 km NE of Nanortalik, Greenland",earthquake,5.1,1.9,0.059,89,reviewed,us,us
2022-01-19T01:52:25.460Z,36.553833,-121.1776657,4.87,1.59,md,17,154,0.01889,0.17,nc,nc73680446,2022-01-19T04:34:10.534Z,"4km NW of Pinnacles, CA",earthquake,0.51,1.15,0.15,12,automatic,nc,nc
2022-01-19T01:51:22.208Z,53.7972,160.5779,66.76,4.5,mb,,137,1.39,0.71,us,us7000gd2g,2022-01-19T02:15:30.040Z,"153 km ENE of Petropavlovsk-Kamchatsky, Russia",earthquake,11.1,8.2,0.106,28,reviewed,us,us
2022-01-19T01:47:47.392Z,-32.6848,-176.9353,10,4.6,mb,,177,3.515,0.55,us,us7000gd2e,2022-01-19T02:05:20.040Z,"south of the Kermadec Islands",earthquake,10.3,1.8,0.193,10,reviewed,us,us
2022-01-19T01:46:43.270Z,17.928,-66.9028,5,3.08,md,24,192,0.0527,0.15,pr,pr2022019001,2022-01-19T23:30:31.358Z,"4 km S of Guánica, Puerto Rico",earthquake,0.39,0.27,0.21,20,reviewed,pr,pr
2022-01-19T01:42:21.410Z,33.4788333,-116.4363333,14.29,0.72,ml,33,76,0.04533,0.13,ci,ci39916279,2022-01-19T18:37:14.180Z,"24km ESE of Anza, CA",earthquake,0.19,0.39,0.086,19,reviewed,ci,ci
2022-01-19T01:37:40.360Z,19.2113342285156,-155.418167114258,33.5499992370605,2.09,ml,44,143,,0.109999999,hv,hv72880767,2022-01-19T01:43:15.160Z,"6 km E of Pāhala, Hawaii",earthquake,0.63,0.850000024,4.61,4,automatic,hv,hv
2022-01-19T01:32:14.820Z,33.4801667,-116.434,12.76,0.45,ml,23,77,0.04367,0.13,ci,ci39916271,2022-01-19T18:28:57.983Z,"23km SSW of La Quinta, CA",earthquake,0.28,0.61,0.121,11,reviewed,ci,ci
2022-01-19T01:31:54.360Z,33.67,-116.7715,15.73,-0.01,ml,13,126,0.06302,0.07,ci,ci37379820,2022-01-19T18:33:06.050Z,"9km SSW of Idyllwild, CA",earthquake,0.24,0.34,0.065,6,reviewed,ci,ci
2022-01-19T01:24:31.510Z,62.9418,-148.5017,0,2.3,ml,,,,0.91,ak,ak022vfy8k3,2022-01-19T01:35:13.578Z,"55 km SSE of Cantwell, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-19T01:22:12.710Z,38.7994995,-122.8365021,1.5,0.62,md,13,77,0.005983,0.02,nc,nc73680441,2022-01-19T01:23:46.716Z,"7km WNW of The Geysers, CA",earthquake,0.28,0.43,0.23,3,automatic,nc,nc
2022-01-19T01:16:39.983Z,-20.8291,-175.3305,10,4.8,mb,,146,6.961,0.79,us,us7000gd26,2022-01-19T15:27:27.040Z,"36 km NNW of Nuku‘alofa, Tonga",earthquake,11.6,1.9,0.058,97,reviewed,us,us
2022-01-19T01:13:26.260Z,36.7395,-116.0284,2.9,0.2,ml,11,124.43,0.036,0.1689,nn,nn00831910,2022-01-19T18:09:59.546Z,"37 km WNW of Indian Springs, Nevada",earthquake,,2.8,0.24,7,reviewed,nn,nn
2022-01-19T01:10:10.370Z,39.4206667,-110.3086667,-1.96,1.87,md,7,196,0.01318,0.11,uu,uu60478017,2022-01-19T16:14:36.740Z,"16 km SSE of Sunnyside, Utah",earthquake,1.06,1.07,0.116,7,reviewed,uu,uu
2022-01-19T01:02:04.040Z,35.695,-117.48,4.69,0.35,ml,7,146,0.1092,0.06,ci,ci39916255,2022-01-19T18:42:59.313Z,"11km SW of Searles Valley, CA",earthquake,0.4,0.51,0.052,4,reviewed,ci,ci
2022-01-19T01:00:40.600Z,38.8019981,-122.7716675,1.21,0.35,md,11,96,0.009442,0.02,nc,nc73680431,2022-01-19T01:02:16.447Z,"3km NNW of The Geysers, CA",earthquake,0.32,0.59,,1,automatic,nc,nc
2022-01-19T00:57:46.800Z,39.4283333,-110.32,-1.43,2.14,ml,17,108,0.005786,0.11,uu,uu60478012,2022-01-19T17:11:03.310Z,"14 km SSE of Sunnyside, Utah",earthquake,0.41,0.17,0.077,4,reviewed,uu,uu
2022-01-19T00:57:35.629Z,38.1505,-117.9734,11.1,1.3,ml,17,119.61,0.016,0.1414,nn,nn00831907,2022-01-19T17:26:23.412Z,"29 km SSE of Mina, Nevada",earthquake,,0.9,0.28,7,reviewed,nn,nn
2022-01-19T00:53:50.460Z,33.476,-116.4326667,14.32,0.75,ml,29,77,0.04763,0.18,ci,ci39916239,2022-01-19T18:26:02.750Z,"24km SSW of La Quinta, CA",earthquake,0.31,0.51,0.116,15,reviewed,ci,ci
2022-01-19T00:49:47.750Z,19.1486663818359,-155.378494262695,31.1599998474121,1.82000005,md,38,214,,0.0900000036,hv,hv72880722,2022-01-19T00:53:02.180Z,"12 km ESE of Pāhala, Hawaii",earthquake,0.84,1.20000005,,5,automatic,hv,hv
2022-01-19T00:44:49.868Z,38.0985,-118.2203,13.1,1.1,ml,9,195.95,0.271,0.0872,nn,nn00831964,2022-01-20T02:36:43.068Z,"33 km SSW of Mina, Nevada",earthquake,,4.7,0.21,2,reviewed,nn,nn
2022-01-19T00:44:40.780Z,18.0221,-66.8503,17,2.33,md,12,115,0.0552,0.16,pr,pr2022019000,2022-01-19T01:10:42.325Z,"1 km S of Yauco, Puerto Rico",earthquake,0.63,0.49,0.2,10,reviewed,pr,pr
2022-01-19T00:39:02.269Z,63.3338,-145.5308,0,1.3,ml,,,,0.66,ak,ak022vffygy,2022-01-19T00:43:47.908Z,"27 km N of Paxson, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-19T00:36:20.970Z,58.3443333333333,-154.6975,6.3,-0.49,ml,5,230,,0.17,av,av91047423,2022-01-21T01:22:02.860Z,"87 km N of Karluk, Alaska",earthquake,0.76,1.25,0.192970375141126,5,reviewed,av,av
2022-01-19T00:28:18.388Z,38.1794,-117.7512,11.9,1.3,ml,16,121.29,0.108,0.1441,nn,nn00831902,2022-01-19T17:32:37.810Z,"39 km SE of Mina, Nevada",earthquake,,2,0.42,6,reviewed,nn,nn
2022-01-19T00:20:44.400Z,37.6336667,-119.3985,11.49,1.74,md,23,114,0.2534,0.22,nc,nc73680426,2022-01-19T03:44:10.802Z,"20km SE of Yosemite Valley, CA",earthquake,0.61,2.54,0.246,23,reviewed,nc,nc
2022-01-19T00:08:16.540Z,54.5693333333333,-163.351,9.34,1.32,ml,7,270,,0.21,av,av91047428,2022-01-21T02:06:09.030Z,"31 km S of False Pass, Alaska",earthquake,0.97,0.64,0.141018740272384,7,reviewed,av,av
2022-01-19T00:07:18.080Z,45.0121667,-111.9475,3.41,0.58,ml,9,154,0.231,0.21,mb,mb80536379,2022-01-19T16:00:22.150Z,"31 km S of Virginia City, Montana",earthquake,1.28,10.25,0.133,3,reviewed,mb,mb
2022-01-19T00:05:36.524Z,64.9626,-147.4043,2.7,1.6,ml,,,,0.71,ak,ak022vf8qrj,2022-01-19T00:12:24.737Z,"10 km E of Fox, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T23:58:51.340Z,60.1423,-153.264,150.5,1.7,ml,,,,0.81,ak,ak022u5pr7e,2022-01-19T00:03:13.217Z,"58 km E of Port Alsworth, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-18T23:49:15.048Z,-20.6214,-175.3924,10,4.8,mb,,124,6.823,0.79,us,us7000ge5h,2022-01-22T05:06:34.040Z,"60 km NNW of Nuku‘alofa, Tonga",earthquake,14.5,1.9,0.072,60,reviewed,us,us
2022-01-18T23:43:01.730Z,34.9903333,-118.1926667,-0.82,1.41,ml,20,57,0.1151,0.18,ci,ci39916183,2022-01-19T18:50:03.900Z,"7km SSW of Mojave, CA",quarry blast,0.37,31.61,0.098,28,reviewed,ci,ci
2022-01-18T23:36:27.039Z,56.8363,-154.6124,16.2,1.7,ml,,,,0.51,ak,ak022u5l0be,2022-01-19T00:04:53.511Z,"29 km WSW of Akhiok, Alaska",earthquake,,2.8,,,reviewed,ak,ak
2022-01-18T23:25:58.710Z,34.3005,-116.8393333,2.15,1.02,ml,16,78,0.04841,0.12,ci,ci39916175,2022-01-19T18:45:49.401Z,"4km N of Big Bear City, CA",earthquake,0.2,0.28,0.136,13,reviewed,ci,ci
2022-01-18T23:25:32.660Z,58.2898333333333,-154.984333333333,2.82,-0.15,ml,10,199,,0.13,av,av91466416,2022-01-20T04:03:42.250Z,"86 km NNW of Karluk, Alaska",earthquake,0.58,0.63,0.229410131768227,10,reviewed,av,av
2022-01-18T23:24:46.130Z,61.3527,-140.9808,13.1,1.3,ml,,,,0.12,ak,ak022u5igjp,2022-01-18T23:33:39.934Z,"104 km E of McCarthy, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T23:17:23.780Z,46.8485,-121.7615,0.64,0.32,ml,16,68,0.02172,0.07,uw,uw61802642,2022-01-20T02:27:15.000Z,"22 km ENE of Ashford, Washington",earthquake,0.22,0.47,0.199192886907329,8,reviewed,uw,uw
2022-01-18T23:12:24.011Z,62.0242,-149.3887,46.2,1.2,ml,,,,0.68,ak,ak022u5fu8x,2022-01-18T23:17:18.084Z,"28 km ESE of Susitna North, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-18T23:06:02.940Z,44.621,-112.0801667,12.83,0.91,ml,8,134,0.226,0.14,mb,mb80536374,2022-01-19T15:51:20.030Z,"30 km NNE of Spencer, Idaho",earthquake,0.94,2.49,0.16,4,reviewed,mb,mb
2022-01-18T22:59:52.050Z,35.7128333,-117.5078333,3.17,0.87,ml,16,102,0.126,0.13,ci,ci39916135,2022-01-19T18:19:20.242Z,"11km WSW of Searles Valley, CA",earthquake,0.32,1.27,0.157,10,reviewed,ci,ci
2022-01-18T22:50:43.220Z,38.793499,-122.7649994,2.93,0.36,md,8,105,0.008228,0.01,nc,nc73680406,2022-01-18T22:52:17.703Z,"2km NNW of The Geysers, CA",earthquake,0.5,1.37,,1,automatic,nc,nc
2022-01-18T22:46:48.990Z,35.6921667,-117.4453333,5.16,-0.35,ml,3,215,0.1063,0.02,ci,ci39916119,2022-01-19T18:40:53.954Z,"9km SSW of Searles Valley, CA",earthquake,1,4.4,0.111,1,reviewed,ci,ci
2022-01-18T22:46:20.859Z,36.0958,71.1049,85.82,4.4,mb,,97,1.112,1.01,us,us7000gd0v,2022-01-18T23:24:05.040Z,"75 km SSW of Ashkāsham, Afghanistan",earthquake,8.7,6.4,0.068,62,reviewed,us,us
2022-01-18T22:42:22.010Z,33.8341667,-118.275,9.04,1.55,ml,18,77,0.03502,0.22,ci,ci39916111,2022-01-19T17:51:47.807Z,"1km ENE of Carson, CA",earthquake,0.44,0.64,0.3,22,reviewed,ci,ci
2022-01-18T22:40:12.120Z,38.8238335,-122.8531647,2.49,1.2,md,26,63,0.004704,0.02,nc,nc73680401,2022-01-19T00:59:12.689Z,"10km WNW of The Geysers, CA",earthquake,0.2,0.41,0.03,4,automatic,nc,nc
2022-01-18T22:18:57.740Z,35.6721667,-117.5325,4.88,1.88,ml,25,68,0.1029,0.16,ci,ci39916095,2022-01-19T14:34:08.836Z,"14km ENE of Ridgecrest, CA",earthquake,0.27,0.77,0.21,26,reviewed,ci,ci
2022-01-18T22:13:43.440Z,38.8346672,-122.809166,2.23,1.18,md,16,55,0.01517,0.01,nc,nc73680386,2022-01-18T23:51:10.339Z,"8km W of Cobb, CA",earthquake,0.24,0.59,0.3,4,automatic,nc,nc
2022-01-18T22:01:11.870Z,-20.9345,-175.3681,10,4.6,mb,,146,6.974,0.55,us,us7000gde9,2022-01-22T04:54:09.040Z,"28 km NW of Nuku‘alofa, Tonga",earthquake,12.3,1.9,0.137,16,reviewed,us,us
2022-01-18T21:56:50.073Z,-2.6435,-78.7703,70.2,4.2,mb,,120,1.146,0.96,us,us7000gd0q,2022-01-18T22:43:29.040Z,"13 km NE of Azogues, Ecuador",earthquake,5.1,16.1,0.137,15,reviewed,us,us
2022-01-18T21:51:14.379Z,38.3091,-118.7825,0,0.8,ml,7,324.92,0.226,0.0308,nn,nn00831919,2022-01-19T02:38:27.623Z,"27 km SSW of Hawthorne, Nevada",earthquake,,0,0,1,reviewed,nn,nn
2022-01-18T21:41:53.120Z,39.4246667,-110.3188333,-1.21,1.13,md,5,192,0.004887,0.01,uu,uu60477997,2022-01-19T15:58:40.160Z,"15 km SSE of Sunnyside, Utah",earthquake,1.68,0.35,0.248,5,reviewed,uu,uu
2022-01-18T21:08:01.430Z,19.203332901001,-155.423004150391,33.5,1.84000003,md,37,145,,0.109999999,hv,hv72880557,2022-01-18T21:11:20.070Z,"5 km E of Pāhala, Hawaii",earthquake,0.61,0.920000017,1.40999997,6,automatic,hv,hv
2022-01-18T21:06:09.999Z,38.1577,-117.8762,10.4,1.8,ml,18,110.03,0.068,0.124,nn,nn00831879,2022-01-19T02:38:03.329Z,"32 km SE of Mina, Nevada",earthquake,,1.1,0.25,7,reviewed,nn,nn
2022-01-18T21:05:46.060Z,44.7866667,-110.8158333,5.6,0.48,md,6,268,0.02474,0.1,uu,uu60477987,2022-01-18T22:21:31.740Z,"22 km SSW of Mammoth, Wyoming",earthquake,1.58,1.36,0.689,5,reviewed,uu,uu
2022-01-18T20:59:15.020Z,35.8036667,-117.6223333,6.87,0.15,ml,7,125,0.0235,0.04,ci,ci39916047,2022-01-19T18:38:19.162Z,"20km WNW of Searles Valley, CA",earthquake,0.17,0.3,0.159,4,reviewed,ci,ci
2022-01-18T20:54:05.860Z,38.8151667,-122.8145,3.02,0.15,md,21,48,0.008914,0.03,nc,nc73680376,2022-01-19T08:52:17.874Z,"7km NW of The Geysers, CA",earthquake,0.21,0.44,0.322,3,reviewed,nc,nc
2022-01-18T20:42:36.105Z,59.8555,-153.0994,125.4,1.2,ml,,,,0.69,ak,ak022u3tzt1,2022-01-18T20:49:24.216Z,"56 km E of Pedro Bay, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-18T20:42:23.040Z,41.2368333,-111.6338333,4.22,1.09,md,15,117,0.2082,0.12,uu,uu60477977,2022-01-18T22:53:22.040Z,"11 km ESE of Huntsville, Utah",earthquake,0.32,4.14,0.181,12,reviewed,uu,uu
2022-01-18T20:40:00.950Z,36.1418333,-91.0651667,12.82,1.62,md,5,228,0.1016,0.01,nm,nm60143243,2022-01-19T17:26:50.930Z,"4 km NE of Black Rock, Arkansas",earthquake,1.46,1.06,0.021,3,reviewed,nm,nm
2022-01-18T20:37:16.570Z,51.8783333333333,-176.594333333333,4.5,1.12,ml,4,260,,0.1,av,av91047418,2022-01-20T03:43:52.730Z,"2 km E of Adak, Alaska",earthquake,1.02,0.61,0.263270264034777,5,reviewed,av,av
2022-01-18T20:28:29.750Z,34.0611667,-117.2658333,16.57,1.66,ml,75,24,0.04632,0.15,ci,ci39916023,2022-01-19T17:44:24.840Z,"2km NNW of Loma Linda, CA",earthquake,0.13,0.3,0.124,58,reviewed,ci,ci
2022-01-18T20:26:57.500Z,35.9405,-119.7616667,20.64,1.75,md,28,125,0.3158,0.17,nc,nc73680371,2022-01-19T01:28:11.894Z,"20km ESE of Kettleman City, CA",earthquake,0.86,0.93,0.187,21,reviewed,nc,nc
2022-01-18T20:17:46.732Z,-20.4833,-175.3586,10,4.7,mb,,188,6.798,0.29,us,us7000ge57,2022-01-22T04:38:52.040Z,"74 km NNW of Nuku‘alofa, Tonga",earthquake,11.7,1.9,0.143,15,reviewed,us,us
2022-01-18T20:16:10.340Z,36.5073318,-121.0753326,8.36,0.93,md,4,142,0.0538,0,nc,nc73680366,2022-01-18T20:18:17.622Z,"7km ESE of Pinnacles, CA",earthquake,1.21,1.33,0.35,3,automatic,nc,nc
2022-01-18T20:03:28.144Z,64.963,-148.9528,16.3,0.9,ml,,,,0.35,ak,ak022u3lmb4,2022-01-18T20:07:10.212Z,"28 km SE of Minto, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T20:01:06.670Z,36.7331,-116.0356,6.5,-0.3,ml,7,160.27,0.041,0.08,nn,nn00831899,2022-01-19T02:38:16.206Z,"37 km WNW of Indian Springs, Nevada",earthquake,,2.4,0.12,3,reviewed,nn,nn
2022-01-18T19:59:20.800Z,34.2698333,-116.7243333,4.88,1.16,ml,32,58,0.1156,0.1,ci,ci39915991,2022-01-19T18:06:33.558Z,"11km E of Big Bear City, CA",earthquake,0.17,0.84,0.111,26,reviewed,ci,ci
2022-01-18T19:52:37.300Z,38.8361664,-122.8123322,0.69,0.85,md,12,58,0.01287,0.01,nc,nc73680361,2022-01-18T19:54:14.707Z,"8km WNW of Cobb, CA",earthquake,0.22,0.75,,1,automatic,nc,nc
2022-01-18T19:49:48.638Z,62.9016,-148.4251,1,1.7,ml,,,,0.65,ak,ak022u3a36x,2022-01-18T19:52:28.697Z,"60 km SSE of Cantwell, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T19:39:56.890Z,46.8843333,-112.5195,10.9,1.2,ml,13,64,0.05,0.13,mb,mb80536309,2022-01-18T21:08:27.210Z,"14 km ESE of Lincoln, Montana",earthquake,0.39,0.69,0.137,5,reviewed,mb,mb
2022-01-18T19:29:58.090Z,46.1993333333333,-122.184666666667,2.92,0.64,ml,14,84,0.001042,0.11,uw,uw61802537,2022-01-19T17:48:08.380Z,"38 km NNE of Amboy, Washington",earthquake,0.31,0.48,0.239200568224524,6,reviewed,uw,uw
2022-01-18T19:10:05.593Z,21.2532,122.007,189.39,4.7,mww,,53,1.778,0.95,us,us7000gczf,2022-01-20T20:06:39.911Z,"89 km N of Basco, Philippines",earthquake,7.7,5,0.073,18,reviewed,us,us
2022-01-18T19:08:03.780Z,38.7895012,-122.7626648,1.86,1.06,md,17,65,0.01134,0.03,nc,nc73680351,2022-01-18T19:09:41.438Z,"2km NNW of The Geysers, CA",earthquake,0.27,0.5,0.11,4,automatic,nc,nc
2022-01-18T18:59:11.540Z,34.2718333,-116.7276667,5.56,2.47,ml,77,28,0.1122,0.12,ci,ci39915959,2022-01-20T19:47:42.040Z,"11km E of Big Bear City, CA",earthquake,0.1,0.44,0.185,25,reviewed,ci,ci
2022-01-18T18:57:02.248Z,62.3134,-151.2277,74.8,1.8,ml,,,,0.72,ak,ak022u2q9qa,2022-01-18T19:08:03.294Z,"31 km SW of Petersville, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-18T18:55:20.140Z,35.919,-117.7278333,10.06,0.6,ml,15,56,0.06916,0.16,ci,ci39915951,2022-01-19T18:12:40.449Z,"16km E of Little Lake, CA",earthquake,0.3,0.75,0.102,5,reviewed,ci,ci
2022-01-18T18:47:22.499Z,61.2502,-146.827,15.4,2.3,ml,,,,0.76,ak,ak022u2o649,2022-01-20T19:33:40.040Z,"28 km WNW of Valdez, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T18:33:18.405Z,36.781,-116.1113,2.5,-0.3,ml,7,200.26,0.021,0.1641,nn,nn00831898,2022-01-19T02:38:15.268Z,"45 km WNW of Indian Springs, Nevada",earthquake,,2.4,0.24,3,reviewed,nn,nn
2022-01-18T18:22:54.239Z,61.3177,-149.9534,24.4,1.3,ml,,,,0.58,ak,ak022u2ivm8,2022-01-18T18:36:38.659Z,"4 km SSE of Point MacKenzie, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-18T18:21:48.540Z,35.8916667,-117.6588333,3.25,1.26,ml,16,56,0.05653,0.1,ci,ci39915887,2022-01-18T18:41:22.409Z,"23km ESE of Little Lake, CA",earthquake,0.19,0.6,0.109,17,reviewed,ci,ci
2022-01-18T18:15:03.960Z,38.8128319,-122.7963333,2.66,0.96,md,23,39,0.004923,0.02,nc,nc73680321,2022-01-18T18:16:41.947Z,"5km NW of The Geysers, CA",earthquake,0.21,0.48,0.17,3,automatic,nc,nc
2022-01-18T18:14:10.620Z,38.8253326,-122.8539963,2.3,0.36,md,14,62,0.003151,0.02,nc,nc73680316,2022-01-18T18:15:46.906Z,"10km WNW of The Geysers, CA",earthquake,0.25,0.43,0.01,3,automatic,nc,nc
2022-01-18T18:07:55.380Z,18.0196,-66.8695,14,1.91,md,5,246,0.0455,0.2,pr,pr2022018009,2022-01-18T19:59:47.465Z,"0 km NNE of Palomas, Puerto Rico",earthquake,1.17,1.09,0.16,5,reviewed,pr,pr
2022-01-18T18:06:47.376Z,-63.1832,-160.5146,10,5.4,mww,,50,17.857,0.77,us,us7000gcz4,2022-01-20T19:09:43.298Z,"Pacific-Antarctic Ridge",earthquake,12.5,1.8,0.098,10,reviewed,us,us
2022-01-18T18:04:18.100Z,46.1973333333333,-122.193166666667,3.07,0,ml,8,103,0.006048,0.07,uw,uw61802492,2022-01-20T05:15:53.200Z,"37 km NNE of Amboy, Washington",earthquake,0.34,0.53,0.104076515277732,4,reviewed,uw,uw
2022-01-18T18:01:02.730Z,45.2256667,-112.3143333,-2,0.58,ml,9,81,0.194,0.14,mb,mb80536329,2022-01-18T20:55:27.440Z,"19 km SW of Alder, Montana",quarry blast,0.5,31.61,0.271,2,reviewed,mb,mb
2022-01-18T17:59:54.607Z,-20.6508,-175.6063,10,4.9,mb,,124,6.652,0.71,us,us7000gcz2,2022-01-19T16:26:46.040Z,"68 km NW of Nuku‘alofa, Tonga",earthquake,9.1,1.7,0.059,94,reviewed,us,us
2022-01-18T17:58:49.780Z,19.2059993743896,-155.415664672852,34.8300018310547,2.02999997,md,43,149,,0.119999997,hv,hv72880302,2022-01-18T18:02:03.070Z,"6 km E of Pāhala, Hawaii",earthquake,0.55,0.790000021,0.589999974,21,automatic,hv,hv
2022-01-18T17:47:24.913Z,40.0982,-119.6698,14.4,0.2,ml,3,184.06,0.086,0.0137,nn,nn00831918,2022-01-19T02:38:26.883Z,"17 km NNW of Sutcliffe, Nevada",earthquake,,5.7,0.08,2,reviewed,nn,nn
2022-01-18T17:41:54.670Z,39.4245,-110.3146667,-1.27,1.69,md,7,194,0.008091,0.07,uu,uu60477957,2022-01-18T17:59:57.450Z,"15 km SSE of Sunnyside, Utah",earthquake,1,0.32,0.143,7,reviewed,uu,uu
2022-01-18T17:41:26.913Z,31.71714818,-104.5145795,4.589086914,2.4,ml,23,91,0.03591339812,0.3,tx,tx2022bgkp,2022-01-20T17:40:00.040Z,"52 km SSW of Whites City, New Mexico",earthquake,1.43835385,0.8214290669999998,0.2,11,reviewed,tx,tx
2022-01-18T17:38:32.310Z,35.6955,-117.526,10.12,1.16,ml,23,97,0.1199,0.11,ci,ci39915847,2022-01-18T22:03:58.239Z,"14km SW of Searles Valley, CA",earthquake,0.23,0.59,0.147,12,reviewed,ci,ci
2022-01-18T17:34:23.450Z,36.0841667,-117.8663333,2.38,1.09,ml,15,140,0.03461,0.12,ci,ci39915839,2022-01-18T18:41:56.832Z,"9km ENE of Coso Junction, CA",earthquake,0.27,0.17,0.201,14,reviewed,ci,ci
2022-01-18T17:33:46.760Z,38.8326683,-122.8131638,2.2,0.97,md,26,51,0.009569,0.02,nc,nc73680301,2022-01-18T17:35:24.769Z,"8km NW of The Geysers, CA",earthquake,0.19,0.42,0.09,4,automatic,nc,nc
2022-01-18T17:31:33.280Z,38.8330002,-122.8131638,2.39,0.65,md,20,52,0.00989,0.02,nc,nc73680296,2022-01-18T17:33:10.779Z,"8km W of Cobb, CA",earthquake,0.23,0.56,0.08,3,automatic,nc,nc
2022-01-18T17:28:53.789Z,37.4526,142.0478,34.01,4.4,mb,,67,3.204,0.86,us,us7000gcxq,2022-01-20T18:55:36.802Z,"92 km E of Namie, Japan",earthquake,5.4,5.4,0.079,53,reviewed,us,us
2022-01-18T17:24:13.745Z,38.1775,-119.1698,14.8,1.2,ml,9,142.56,0.273,0.1252,nn,nn00831917,2022-01-19T02:38:26.134Z,"10 km SSE of Bridgeport, California",earthquake,,2.7,0.13,3,reviewed,nn,nn
2022-01-18T17:22:59.970Z,33.5908333,-116.8061667,6.92,-0.06,ml,11,164,0.03523,0.06,ci,ci39915823,2022-01-18T22:18:32.786Z,"13km WNW of Anza, CA",earthquake,0.22,0.36,0.096,3,reviewed,ci,ci
2022-01-18T17:22:41.307Z,61.3604,-150.7014,33.7,1.6,ml,,,,0.74,ak,ak022u1xf42,2022-01-18T18:15:21.358Z,"22 km SSW of Susitna, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T17:15:51.810Z,19.1841659545898,-155.479507446289,37.6399993896484,2.24000001,md,47,78,,0.0900000036,hv,hv72880242,2022-01-18T17:19:11.170Z,"2 km S of Pāhala, Hawaii",earthquake,0.53,0.689999998,1.13999999,19,automatic,hv,hv
2022-01-18T17:15:00.780Z,33.4908333,-116.4823333,14.96,0.17,ml,10,128,0.05739,0.16,ci,ci39915807,2022-01-18T22:16:25.950Z,"19km ESE of Anza, CA",earthquake,0.8,1.12,0.026,2,reviewed,ci,ci
2022-01-18T17:13:02.719Z,32.0535,138.0027,359.45,4.2,mb,,75,1.859,0.47,us,us7000gcxl,2022-01-18T21:32:46.040Z,"265 km SE of Shingū, Japan",earthquake,5.5,7,0.042,160,reviewed,us,us
2022-01-18T17:09:38.634Z,60.7972,-149.8351,28.7,1.4,ml,,,,0.6,ak,ak022u1umlj,2022-01-18T18:15:21.219Z,"Kenai Peninsula, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T17:06:33.250Z,36.7340012,-121.3616638,4.76,1.73,md,20,162,0.02915,0.07,nc,nc73680291,2022-01-18T18:58:11.170Z,"7km SSW of Tres Pinos, CA",earthquake,0.35,0.82,0.19,19,automatic,nc,nc
2022-01-18T17:06:31.960Z,45.3011666666667,-121.731,1.67,0.64,ml,6,186,0.0375,0.08,uw,uw61802447,2022-01-18T20:05:44.760Z,"1 km E of Government Camp, Oregon",earthquake,0.37,10.51,0.104673720922085,4,reviewed,uw,uw
2022-01-18T17:03:36.150Z,38.7771667,-122.7275,1.69,0.38,md,20,59,0.00942,0.03,nc,nc73680286,2022-01-20T22:10:18.869Z,"2km E of The Geysers, CA",earthquake,0.21,0.4,0.257,3,reviewed,nc,nc
2022-01-18T16:59:27.989Z,39.2481,-120.1177,8.7,0.2,ml,6,114.45,0.041,0.078,nn,nn00831916,2022-01-19T02:38:25.164Z,"3 km NW of Carnelian Bay, California",earthquake,,1.7,0.23,3,reviewed,nn,nn
2022-01-18T16:51:05.160Z,-20.7979,-175.4352,10,4.6,mb,,124,6.859,0.61,us,us7000ge50,2022-01-22T04:19:50.040Z,"44 km NNW of Nuku‘alofa, Tonga",earthquake,10.6,1.9,0.173,10,reviewed,us,us
2022-01-18T16:50:25.330Z,40.3806667,-124.769,18.84,2.71,md,39,245,0.3387,0.16,nc,nc73680281,2022-01-18T21:29:11.433Z,"42km W of Petrolia, CA",earthquake,1.11,0.57,0.144,34,reviewed,nc,nc
2022-01-18T16:49:44.879Z,-57.4097,147.7845,8.31,5.1,mb,,102,6.917,0.58,us,us7000gcxi,2022-01-18T17:25:26.040Z,"west of Macquarie Island",earthquake,11.2,6.2,0.093,39,reviewed,us,us
2022-01-18T16:44:52.312Z,40.1689,-119.6425,10,0.7,ml,4,245.64,0.069,0.1296,nn,nn00831915,2022-01-19T02:38:24.274Z,"24 km N of Sutcliffe, Nevada",earthquake,,3,0.26,4,reviewed,nn,nn
2022-01-18T16:43:24.930Z,19.1604995727539,-155.497833251953,31.2800006866455,1.70000005,md,40,124,,0.150000006,hv,hv72880202,2022-01-18T16:46:47.920Z,"5 km SSW of Pāhala, Hawaii",earthquake,0.63,1.05999994,0.720000029,3,automatic,hv,hv
2022-01-18T16:39:36.950Z,37.427,-112.983,8.04,1.19,ml,7,162,0.1337,0.07,uu,uu60477952,2022-01-18T17:57:52.660Z,"Utah",earthquake,0.65,2.11,0.073,3,reviewed,uu,uu
2022-01-18T16:34:57.862Z,-19.6448,-69.2154,102.48,4.3,mb,,80,0.03,0.54,us,us7000gcxf,2022-01-18T18:07:50.627Z,"116 km ENE of Iquique, Chile",earthquake,6.3,3.7,0.147,14,reviewed,us,us
2022-01-18T16:30:31.140Z,38.8341675,-122.8108368,2.15,0.83,md,21,56,0.01077,0.01,nc,nc73680256,2022-01-18T16:32:08.547Z,"8km W of Cobb, CA",earthquake,0.22,0.43,0.24,4,automatic,nc,nc
2022-01-18T16:26:04.951Z,62.711,-150.9518,84.2,1.5,ml,,,,0.39,ak,ak022u1crkf,2022-01-18T16:29:49.138Z,"25 km NNW of Petersville, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-18T16:23:48.736Z,-19.8218,-69.1094,120.48,4.4,mb,,71,0.172,0.58,us,us7000gcxc,2022-01-19T00:20:22.990Z,"117 km ENE of Iquique, Chile",earthquake,6.3,2.5,0.107,27,reviewed,us,us
2022-01-18T16:22:54.810Z,38.8363342,-122.8059998,2.02,0.36,md,9,81,0.0124,0.01,nc,nc73680251,2022-01-18T16:24:29.779Z,"7km WNW of Cobb, CA",earthquake,0.45,0.97,,1,automatic,nc,nc
2022-01-18T16:21:12.138Z,56.5877,-148.5581,10,3.2,ml,,254,2.497,0.16,us,us7000gcxb,2022-01-18T16:36:00.040Z,"252 km ESE of Chiniak, Alaska",earthquake,4.6,2,0.047,60,reviewed,us,us
2022-01-18T16:19:25.581Z,62.2052,-145.6483,25.1,1.1,ml,,,,0.46,ak,ak022u1bb57,2022-01-18T16:31:59.550Z,"11 km NNW of Glennallen, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-18T16:16:38.947Z,57.8707,-156.1259,127.2,1.6,ml,,,,0.44,ak,ak022u1ap12,2022-01-18T16:26:28.589Z,"83 km ESE of Egegik, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-18T16:14:39.360Z,37.4373333,-112.9778333,4.26,2.22,ml,16,143,0.1428,0.12,uu,uu60477947,2022-01-18T16:36:49.120Z,"21 km ESE of Kanarraville, Utah",earthquake,0.44,3.88,0.159,7,reviewed,uu,uu
2022-01-18T16:09:08.680Z,38.8358333,-122.8155,1.78,-0.08,md,9,95,0.01312,0.02,nc,nc73680246,2022-01-20T22:35:53.062Z,"8km W of Cobb, CA",earthquake,0.44,0.92,0.066,2,reviewed,nc,nc
2022-01-18T16:07:14.858Z,38.1785,-117.9025,8.7,0.9,ml,13,161.53,0.06,0.128,nn,nn00831871,2022-01-19T02:37:57.255Z,"29 km SE of Mina, Nevada",earthquake,,1.8,0.43,5,reviewed,nn,nn
2022-01-18T16:03:04.380Z,46.9018333333333,-121.9115,7.68,0.34,ml,13,97,0.02258,0.11,uw,uw61802442,2022-01-18T17:42:41.690Z,"18 km NNE of Ashford, Washington",earthquake,0.3,0.61,0.103487502636969,4,reviewed,uw,uw
2022-01-18T16:02:02.120Z,58.3348333333333,-154.837,3.89,-0.57,ml,4,210,,0.09,av,av91047408,2022-01-20T03:07:59.840Z,"88 km NNW of Karluk, Alaska",earthquake,1.28,0.74,0.249228865162145,4,reviewed,av,av
2022-01-18T15:55:23.100Z,33.2223333,-116.1855,7.71,1.14,ml,45,73,0.06458,0.17,ci,ci39915743,2022-01-18T21:57:05.303Z,"10km NNW of Ocotillo Wells, CA",earthquake,0.25,0.45,0.138,25,reviewed,ci,ci
2022-01-18T15:54:03.990Z,33.1938333,-116.3803333,15.18,0.52,ml,22,116,0.08033,0.18,ci,ci39915735,2022-01-18T21:50:42.173Z,"7km S of Borrego Springs, CA",earthquake,0.29,0.56,0.175,7,reviewed,ci,ci
2022-01-18T15:53:19.570Z,38.8386667,-122.8086667,2.09,0.28,md,18,53,0.01431,0.04,nc,nc73680236,2022-01-20T22:33:52.800Z,"8km WNW of Cobb, CA",earthquake,0.24,0.38,0.3,2,reviewed,nc,nc
2022-01-18T15:49:16.070Z,37.3276667,-120.0316667,18.94,2.49,md,55,40,0.147,0.22,nc,nc73680231,2022-01-21T00:38:10.908Z,"18km SSW of Mariposa, CA",earthquake,0.29,0.25,0.155,52,reviewed,nc,nc
2022-01-18T15:36:35.880Z,34.012,-118.2186667,16.08,1.32,ml,26,138,0.05664,0.17,ci,ci39915719,2022-01-18T21:44:53.302Z,"3km N of Huntington Park, CA",earthquake,0.34,0.44,0.239,19,reviewed,ci,ci
2022-01-18T15:33:40.732Z,59.246,-153.7076,101.4,1.6,ml,,,,0.54,ak,ak022u0swqh,2022-01-18T16:20:26.918Z,"56 km SE of Pope-Vannoy Landing, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-18T15:31:01.531Z,62.4214,-148.5148,19.4,1.2,ml,,,,0.58,ak,ak022u0se9x,2022-01-18T15:35:21.478Z,"69 km N of Chickaloon, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T15:25:15.930Z,31.7245,-116.2573333,5.23,2.41,ml,14,164,0.375,0.33,ci,ci39915711,2022-01-18T22:21:31.444Z,"29km E of Maneadero, B.C., MX",earthquake,0.69,31.61,0.225,21,reviewed,ci,ci
2022-01-18T15:24:40.580Z,35.6636667,-117.4626667,9.62,1.39,ml,26,97,0.077,0.15,ci,ci39915695,2022-01-18T21:32:42.230Z,"13km SSW of Searles Valley, CA",earthquake,0.27,0.65,0.205,15,reviewed,ci,ci
2022-01-18T15:23:42.740Z,33.193,-116.3908333,13.23,0.69,ml,24,69,0.07818,0.2,ci,ci39915687,2022-01-18T21:28:26.117Z,"7km SSW of Borrego Springs, CA",earthquake,0.31,0.77,0.169,8,reviewed,ci,ci
2022-01-18T15:21:25.608Z,39.0351,-118.1684,9.2,1.2,ml,11,97.98,0.054,0.1435,nn,nn00831913,2022-01-19T02:38:23.013Z,"28 km NW of Gabbs, Nevada",earthquake,,1.5,0.41,3,reviewed,nn,nn
2022-01-18T15:18:31.120Z,60.3201666666667,-152.742166666667,14.27,-0.52,ml,7,332,,0.09,av,av91047403,2022-01-20T03:02:27.620Z,"66 km WNW of Ninilchik, Alaska",earthquake,1.09,0.7,0.184957462495944,7,reviewed,av,av
2022-01-18T15:15:18.641Z,-5.4374,129.8259,195.56,4.3,mb,,83,2.921,0.7,us,us7000gcx4,2022-01-18T16:14:41.040Z,"252 km SSE of Amahai, Indonesia",earthquake,9.7,9.4,0.108,26,reviewed,us,us
2022-01-18T15:03:00.610Z,33.4806667,-116.4526667,11.97,1.64,ml,54,71,0.04821,0.19,ci,ci39915647,2022-01-18T21:25:35.400Z,"22km ESE of Anza, CA",earthquake,0.2,0.42,0.166,26,reviewed,ci,ci
2022-01-18T15:02:55.300Z,33.4856667,-116.4503333,12.56,0.72,ml,32,47,0.04289,0.21,ci,ci39915639,2022-01-18T15:15:06.757Z,"22km ESE of Anza, CA",earthquake,0.3,0.64,0.272,9,reviewed,ci,ci
2022-01-18T15:02:46.770Z,33.4836667,-116.4485,13.96,0.47,ml,15,73,0.04397,0.15,ci,ci39915631,2022-01-18T21:15:36.029Z,"22km ESE of Anza, CA",earthquake,0.36,0.78,0.154,11,reviewed,ci,ci
2022-01-18T15:00:01.220Z,36.4438324,-121.0214996,8.1,1.25,md,8,103,0.0192,0.05,nc,nc73680226,2022-01-18T15:34:11.732Z,"15km SE of Pinnacles, CA",earthquake,0.4,0.71,0.27,5,automatic,nc,nc
2022-01-18T14:48:51.380Z,60.0223333333333,-153.074333333333,1.3,-0.59,ml,4,146,,0.05,av,av91466181,2022-01-20T02:56:55.400Z,"63 km ENE of Pedro Bay, Alaska",earthquake,0.26,0.27,0.114906479430592,4,reviewed,av,av
2022-01-18T14:47:28.199Z,36.7217,-116.0024,5.6,-0.3,ml,7,188.05,0.015,0.1892,nn,nn00831897,2022-01-19T02:38:14.233Z,"34 km WNW of Indian Springs, Nevada",earthquake,,2.5,0.11,3,reviewed,nn,nn
2022-01-18T14:47:21.010Z,37.4246667,-112.9793333,1.68,1.35,ml,11,151,0.135,0.14,uu,uu60477937,2022-01-18T17:50:38.560Z,"22 km SE of Kanarraville, Utah",earthquake,0.62,31.61,0.101,3,reviewed,uu,uu
2022-01-18T14:45:54.647Z,-18.418,-71.0623,35,4.2,mb,,137,0.685,1.15,us,us7000gcx0,2022-01-18T16:02:19.040Z,"80 km W of Arica, Chile",earthquake,8,2,0.216,7,reviewed,us,us
2022-01-18T14:38:51.380Z,45.829,-122.198666666667,2.78,1.12,ml,9,301,0.1857,0.16,uw,uw61802432,2022-01-18T18:15:44.050Z,"16 km ESE of Yacolt, Washington",earthquake,1.19,8.77,0.344811555781098,5,reviewed,uw,uw
2022-01-18T14:38:19.520Z,37.5228333,-118.8403333,3.23,0.37,md,14,235,0.06767,0.04,nc,nc73680216,2022-01-18T16:52:52.862Z,"15km WSW of Toms Place, CA",earthquake,0.74,31.61,0.302,13,reviewed,nc,nc
2022-01-18T14:34:40.540Z,46.856,-121.762,1.31,0.2,ml,10,104,0.02849,0.06,uw,uw61802427,2022-01-20T05:31:26.630Z,"23 km ENE of Ashford, Washington",earthquake,0.25,0.75,0.204041764289038,7,reviewed,uw,uw
2022-01-18T14:33:18.620Z,35.8798333,-117.6865,10.03,0.53,ml,15,74,0.07398,0.05,ci,ci39915607,2022-01-18T21:11:35.778Z,"21km ESE of Little Lake, CA",earthquake,0.16,0.33,0.152,7,reviewed,ci,ci
2022-01-18T14:31:50.827Z,-20.6843,-175.3304,10,4.6,mb,,157,6.901,0.85,us,us7000gdyh,2022-01-21T23:58:27.040Z,"52 km NNW of Nuku‘alofa, Tonga",earthquake,10.9,1.9,0.085,45,reviewed,us,us
2022-01-18T14:30:25.300Z,38.152,-117.894,9.3,0.9,ml,15,134.17,0.053,0.1348,nn,nn00831869,2022-01-19T02:37:56.262Z,"32 km SE of Mina, Nevada",earthquake,,1.3,0.53,5,reviewed,nn,nn
2022-01-18T14:28:03.706Z,63.7609,-150.5736,5.9,1.6,ml,,,,0.64,ak,ak022u06boy,2022-01-18T14:37:24.778Z,"62 km ENE of Denali National Park, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T14:21:27.045Z,63.5784,-146.2975,13.3,1.7,ml,,,,0.99,ak,ak022u04vdl,2022-01-18T14:26:12.894Z,"53 km SW of Fort Greely, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-18T14:17:58.683Z,-5.6682,148.8926,148.35,4.9,mb,,78,3.909,0.67,us,us7000gcw2,2022-01-18T15:30:56.040Z,"93 km NW of Kandrian, Papua New Guinea",earthquake,9.5,7.5,0.049,131,reviewed,us,us
2022-01-18T14:08:28.460Z,38.8226662,-122.7959976,2.53,1.09,md,28,32,0.01102,0.03,nc,nc73680211,2022-01-18T14:10:03.287Z,"6km NW of The Geysers, CA",earthquake,0.21,0.4,0.09,4,automatic,nc,nc
2022-01-18T14:04:41.860Z,36.8041667,-112.942,11.99,1.75,ml,10,160,0.2328,0.23,uu,uu60477932,2022-01-18T17:15:35.600Z,"16 km SSW of Cane Beds, Arizona",earthquake,0.8,1.44,0.11,4,reviewed,uu,uu
2022-01-18T13:51:02.346Z,62.1248,-147.9204,19.4,1.7,ml,,,,0.89,ak,ak022tzpthh,2022-01-18T14:24:32.381Z,"37 km NNW of Glacier View, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T13:48:20.360Z,35.9123333,-117.7178333,2.37,0.86,ml,19,49,0.06524,0.11,ci,ci39915567,2022-01-18T21:09:18.663Z,"17km E of Little Lake, CA",earthquake,0.13,0.2,0.139,11,reviewed,ci,ci
2022-01-18T13:47:24.910Z,35.9113333,-117.7165,2.58,0.57,ml,18,48,0.06489,0.11,ci,ci39915559,2022-01-18T21:06:14.959Z,"17km E of Little Lake, CA",earthquake,0.15,0.27,0.218,7,reviewed,ci,ci
2022-01-18T13:46:05.622Z,31.68060667,-104.3814975,7.391259766,2.3,ml,30,65,0.0998036132,0.3,tx,tx2022bgcu,2022-01-20T03:26:07.195Z,"54 km S of Whites City, New Mexico",earthquake,0.9074135828999998,1.002887082,0.1,12,reviewed,tx,tx
2022-01-18T13:44:14.446Z,36.8407,-115.9808,5.4,-0.3,ml,6,180.67,0.112,0.1289,nn,nn00831896,2022-01-19T02:38:13.385Z,"40 km NW of Indian Springs, Nevada",earthquake,,7.3,0.21,2,reviewed,nn,nn
2022-01-18T13:40:25.010Z,35.3193333,-117.7783333,7.52,0.73,ml,14,92,0.07569,0.1,ci,ci39915551,2022-01-18T21:03:41.038Z,"14km WSW of Johannesburg, CA",earthquake,0.23,0.52,0.158,9,reviewed,ci,ci
2022-01-18T13:35:26.310Z,60.5195,-152.811,3.97,-0.9,ml,7,101,,0.05,av,av91047398,2022-01-20T02:54:09.600Z,"82 km NW of Ninilchik, Alaska",earthquake,0.31,1.11,0.147681415910327,6,reviewed,av,av
2022-01-18T13:32:28.180Z,60.3185,-152.739166666667,15.38,-0.62,ml,7,332,,0.07,av,av91047393,2022-01-20T02:51:09.570Z,"66 km WNW of Ninilchik, Alaska",earthquake,1.11,0.63,0.169950490401039,7,reviewed,av,av
2022-01-18T13:29:26.401Z,61.6554,-148.0195,17.8,1,ml,,,,0.85,ak,ak022tzl5k3,2022-01-18T13:34:26.449Z,"25 km SW of Glacier View, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T13:22:24.772Z,38.1617,-117.8761,8.2,1.1,ml,13,110.52,0.07,0.077,nn,nn00831868,2022-01-19T02:37:55.207Z,"32 km SE of Mina, Nevada",earthquake,,1.8,0.57,5,reviewed,nn,nn
2022-01-18T13:19:28.610Z,38.784832,-122.7366638,2.15,0.46,md,11,82,0.001593,0.02,nc,nc73680206,2022-01-18T13:21:02.276Z,"2km ENE of The Geysers, CA",earthquake,0.3,0.96,0.09,2,automatic,nc,nc
2022-01-18T13:18:39.985Z,29.2038,142.0382,32.44,4.7,mb,,71,4.34,0.43,us,us7000gcvy,2022-01-18T15:22:51.040Z,"Izu Islands, Japan region",earthquake,10.3,5.7,0.077,53,reviewed,us,us
2022-01-18T13:17:17.401Z,-18.5739,-176.5306,10,4.8,mb,,123,5.215,0.76,us,us7000gcvu,2022-01-18T15:06:19.040Z,"266 km WNW of Pangai, Tonga",earthquake,14.4,1.9,0.052,119,reviewed,us,us
2022-01-18T13:09:58.246Z,31.64010963,-104.3897507,5.334619141,2.7,ml,37,63,0.09886982569,0.3,tx,tx2022bgbp,2022-01-19T21:45:52.106Z,"59 km S of Whites City, New Mexico",earthquake,1.335864829,1.312482133,0.1,19,reviewed,tx,tx
2022-01-18T13:05:09.660Z,37.636,-118.8745,5.99,0.16,md,14,100,0.0193,0.06,nc,nc73680201,2022-01-18T16:31:19.968Z,"9km E of Mammoth Lakes, CA",earthquake,0.54,1.04,0.201,13,reviewed,nc,nc
2022-01-18T12:59:49.870Z,33.4741667,-116.5978333,9.32,1.48,ml,51,63,0.02166,0.19,ci,ci39915527,2022-01-18T15:28:15.700Z,"11km SE of Anza, CA",earthquake,0.2,0.46,0.173,27,reviewed,ci,ci
2022-01-18T12:58:31.720Z,38.1861667,-118.8423333,2.67,1.47,md,16,146,0.2736,0.05,nc,nc73680196,2022-01-19T02:37:54.131Z,"15km E of Bodie, CA",earthquake,0.37,31.61,0.089,15,reviewed,nc,nc
2022-01-18T12:52:25.900Z,36.7014,-116.2541,8.4,-0.1,ml,7,181.12,0.043,0.0874,nn,nn00831895,2022-01-19T02:38:12.207Z,"50 km ESE of Beatty, Nevada",earthquake,,1.9,0.2,4,reviewed,nn,nn
2022-01-18T12:43:17.065Z,38.1244,-118.5084,12.7,0,ml,6,330.96,0.127,0.0327,nn,nn00831912,2022-01-19T02:38:21.502Z,"34 km N of Benton, California",earthquake,,23.9,0,1,reviewed,nn,nn
2022-01-18T12:38:24.522Z,39.2191,-120.0731,8.7,-0.4,ml,4,141.94,0.043,0.094,nn,nn00831911,2022-01-19T02:38:20.822Z,"1 km SE of Carnelian Bay, California",earthquake,,3.7,0.05,2,reviewed,nn,nn
2022-01-18T12:36:17.110Z,38.7991676,-122.8040009,0.42,0.84,md,12,82,0.01085,0.02,nc,nc73680186,2022-01-18T12:37:53.479Z,"5km WNW of The Geysers, CA",earthquake,0.25,0.62,,1,automatic,nc,nc
2022-01-18T12:35:48.010Z,59.976,-153.072666666667,-2.32,-0.33,ml,5,137,,0.09,av,av91466096,2022-01-20T02:39:39.930Z,"61 km ENE of Pedro Bay, Alaska",earthquake,0.36,1.76,0.230010219955226,5,reviewed,av,av
2022-01-18T12:33:42.576Z,39.4027,-119.8826,9.8,0.1,ml,9,69.66,0.162,0.203,nn,nn00831909,2022-01-19T02:38:20.049Z,"11 km E of Floriston, California",earthquake,,3.6,0.62,5,reviewed,nn,nn
2022-01-18T12:31:47.890Z,31.59490639,-104.0034312,7.519799805,2.8,ml,17,54,0.07402302508,0.1,tx,tx2022bgaj,2022-01-19T22:44:36.299Z,"36 km NNW of Toyah, Texas",earthquake,0.6912933887,0.7811892664,0.1,7,reviewed,tx,tx
2022-01-18T12:28:18.514Z,36.6111,-116.1522,3.4,-0.2,ml,8,256,0.077,0.0678,nn,nn00831894,2022-01-19T02:38:11.373Z,"43 km W of Indian Springs, Nevada",earthquake,,7.4,0.22,4,reviewed,nn,nn
2022-01-18T12:11:17.260Z,38.8129997,-122.828331,1.95,1.09,md,25,49,0.004178,0.02,nc,nc73680181,2022-01-18T12:12:52.151Z,"7km WNW of The Geysers, CA",earthquake,0.18,0.36,0.16,4,automatic,nc,nc
2022-01-18T12:10:15.020Z,38.8240013,-122.784668,1.69,1.22,md,22,41,0.01117,0.03,nc,nc73680176,2022-01-18T12:43:11.700Z,"5km W of Cobb, CA",earthquake,0.2,0.34,0.06,4,automatic,nc,nc
2022-01-18T12:09:38.732Z,56.4305,-148.8295,10,3.2,ml,,256,2.456,0.23,us,us7000gcvb,2022-01-19T09:23:31.040Z,"247 km ESE of Chiniak, Alaska",earthquake,6,2,0.045,66,reviewed,us,us
2022-01-18T12:02:49.920Z,38.8318329,-122.8115005,1.83,0.85,md,9,89,0.008499,0.01,nc,nc73680171,2022-01-18T12:04:27.935Z,"8km NW of The Geysers, CA",earthquake,0.48,1.48,,1,automatic,nc,nc
2022-01-18T11:59:22.790Z,33.172,-116.4361667,12.01,0.83,ml,30,73,0.09725,0.22,ci,ci39915487,2022-01-18T14:29:16.976Z,"11km SSW of Borrego Springs, CA",earthquake,0.39,0.83,0.219,17,reviewed,ci,ci
2022-01-18T11:54:09.970Z,35.7813333,-117.6008333,8.34,1.02,ml,20,139,0.03444,0.09,ci,ci39915479,2022-01-18T21:00:52.928Z,"18km W of Searles Valley, CA",earthquake,0.18,0.32,0.197,14,reviewed,ci,ci
2022-01-18T11:51:09.562Z,37.0562,-116.2216,4.8,0.1,ml,13,127.51,0.071,0.1366,nn,nn00831892,2022-01-19T02:38:10.472Z,"50 km ENE of Beatty, Nevada",earthquake,,2.4,0.21,8,reviewed,nn,nn
2022-01-18T11:48:43.450Z,19.5471668243408,-155.987335205078,6.07999992370605,1.75999999,md,36,231,,0.219999999,hv,hv72879847,2022-01-19T06:30:25.594Z,"3 km SW of Kahaluu-Keauhou, Hawaii",earthquake,0.83,0.49000001,1.83000004,4,automatic,hv,hv
2022-01-18T11:46:40.487Z,61.5967,-146.3439,22.3,1.5,ml,,,,0.87,ak,ak022tyhymw,2022-01-18T11:50:54.967Z,"49 km SSE of Nelchina, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-18T11:41:21.040Z,19.1928333333333,-155.523166666667,34.21,1.8,ml,51,91,,0.11,hv,hv72879842,2022-01-18T20:09:46.250Z,"4 km WSW of Pāhala, Hawaii",earthquake,0.45,0.54,0.0677980203238342,11,reviewed,hv,hv
2022-01-18T11:37:40.850Z,38.8236656,-122.8116684,2.52,0.35,md,10,78,0.001274,0.01,nc,nc73680166,2022-01-18T11:39:17.523Z,"7km NW of The Geysers, CA",earthquake,0.38,0.93,,1,automatic,nc,nc
2022-01-18T11:33:50.430Z,38.8325005,-122.8125,2.07,0.86,md,20,69,0.009288,0.01,nc,nc73680161,2022-01-18T11:35:27.364Z,"8km NW of The Geysers, CA",earthquake,0.24,0.49,0.03,4,automatic,nc,nc
2022-01-18T11:31:55.030Z,34.4341667,-119.2985,9.63,1.39,ml,30,32,0.03711,0.27,ci,ci39915471,2022-01-18T20:58:46.902Z,"5km WSW of Ojai, CA",earthquake,0.35,0.73,0.196,22,reviewed,ci,ci
2022-01-18T11:24:50.760Z,35.9531667,-117.6788333,5.22,0.76,ml,16,90,0.02368,0.1,ci,ci39915463,2022-01-18T14:30:12.980Z,"21km E of Little Lake, CA",earthquake,0.2,0.46,0.153,9,reviewed,ci,ci
2022-01-18T11:21:36.890Z,19.2229995727539,-155.390167236328,32.0299987792969,1.83000004,md,44,151,,0.119999997,hv,hv72879832,2022-01-18T11:24:51.090Z,"9 km ENE of Pāhala, Hawaii",earthquake,0.54,0.629999995,0.00999999978,5,automatic,hv,hv
2022-01-18T11:17:54.300Z,19.232666015625,-155.399673461914,31.7999992370605,2.21,ml,48,140,,0.140000001,hv,hv72879827,2022-01-18T11:23:24.810Z,"8 km ENE of Pāhala, Hawaii",earthquake,0.45,0.569999993,4.02,5,automatic,hv,hv
2022-01-18T11:16:45.440Z,37.5698333,-118.831,3.55,0.59,md,17,146,0.02021,0.06,nc,nc73680156,2022-01-18T16:22:19.176Z,"13km W of Toms Place, CA",earthquake,0.41,0.62,0.12,14,reviewed,nc,nc
2022-01-18T11:13:39.420Z,19.2293338775635,-155.399169921875,32.1699981689453,1.85000002,md,39,148,,0.129999995,hv,hv72879822,2022-01-18T11:16:45.860Z,"8 km ENE of Pāhala, Hawaii",earthquake,0.49,0.699999988,0.230000004,5,automatic,hv,hv
2022-01-18T11:13:24.620Z,33.4868333,-116.4468333,13.1,0.11,ml,18,73,0.04052,0.13,ci,ci39915455,2022-01-18T20:54:27.572Z,"22km ESE of Anza, CA",earthquake,0.26,0.76,0.074,6,reviewed,ci,ci
2022-01-18T11:10:45.350Z,33.4845,-116.447,12.56,0.48,ml,12,110,0.1011,0.07,ci,ci39915447,2022-01-18T14:30:16.980Z,"22km ESE of Anza, CA",earthquake,0.28,0.74,0.257,4,reviewed,ci,ci
2022-01-18T11:08:51.800Z,33.4873333,-116.4441667,13.47,0.57,ml,14,110,0.1008,0.13,ci,ci39915439,2022-01-18T14:30:49.455Z,"23km ESE of Anza, CA",earthquake,0.36,0.87,0.194,8,reviewed,ci,ci
2022-01-18T11:03:55.050Z,-20.6174,-175.6148,10,4.6,mb,,124,6.631,0.33,us,us7000gcuy,2022-01-19T15:27:11.040Z,"72 km NW of Nuku‘alofa, Tonga",earthquake,12.6,1.9,0.073,57,reviewed,us,us
2022-01-18T10:58:16.335Z,36.644,-116.2722,7,-0.3,ml,7,201.96,0.054,0.0839,nn,nn00831891,2022-01-19T02:38:09.452Z,"52 km SE of Beatty, Nevada",earthquake,,2.6,0.18,3,reviewed,nn,nn
2022-01-18T10:54:04.737Z,59.9898,-140.4685,5.9,1.4,ml,,,,0.88,ak,ak022txy5yx,2022-01-18T11:06:59.963Z,"64 km NW of Yakutat, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T10:52:45.260Z,33.9466667,-118.374,13.94,0.98,ml,22,77,0.03928,0.21,ci,ci39915431,2022-01-18T20:51:40.876Z,"2km WNW of Lennox, CA",earthquake,0.59,0.45,0.239,17,reviewed,ci,ci
2022-01-18T10:50:28.109Z,61.004,-148.0968,21.2,0.9,ml,,,,0.39,ak,ak022txxcfi,2022-01-18T19:17:24.516Z,"40 km NE of Whittier, Alaska",earthquake,,0.4,,,reviewed,ak,ak
2022-01-18T10:48:59.850Z,46.8538333333333,-121.758666666667,0.76,1.03,ml,18,74,0.02534,0.09,uw,uw61802397,2022-01-18T18:24:11.010Z,"23 km ENE of Ashford, Washington",earthquake,0.21,0.91,0.197316994172614,7,reviewed,uw,uw
2022-01-18T10:48:35.490Z,38.7908325,-122.7594986,1.67,0.85,md,10,82,0.00978,0.03,nc,nc73680146,2022-01-18T10:50:14.215Z,"2km N of The Geysers, CA",earthquake,0.58,1.51,,1,automatic,nc,nc
2022-01-18T10:47:08.186Z,39.2457,-120.1192,9.5,0.9,ml,17,71.5,0.039,0.1671,nn,nn00831863,2022-01-19T02:37:52.260Z,"3 km WNW of Carnelian Bay, California",earthquake,,1.1,0.22,8,reviewed,nn,nn
2022-01-18T10:36:10.620Z,33.5898333,-116.807,7.61,-0.05,ml,13,85,0.03601,0.07,ci,ci39915423,2022-01-18T20:46:04.151Z,"13km WNW of Anza, CA",earthquake,0.24,0.35,0.224,5,reviewed,ci,ci
2022-01-18T10:31:16.994Z,32.44445801,-102.0796018,1.809651693,3,ml,46,59,0.25437889,0.3,tx,tx2022bfwj,2022-01-21T08:25:44.433Z,"34 km SSW of Los Ybanez, Texas",earthquake,1.139336324,0.9685572483,0.1,27,reviewed,tx,tx
2022-01-18T10:29:17.271Z,62.258,-149.3739,49.9,1.3,ml,,,,1.16,ak,ak022txsu1y,2022-01-18T10:32:35.868Z,"Central Alaska",earthquake,,2.1,,,automatic,ak,ak
2022-01-18T10:18:29.361Z,-22.8547,-69.0666,115.41,4,mb,,84,0.489,0.51,us,us7000gcun,2022-01-18T12:16:39.040Z,"46 km SSW of Calama, Chile",earthquake,4.7,3.4,0.144,13,reviewed,us,us
2022-01-18T10:17:32.452Z,63.3013,-151.2624,1,1.7,ml,,,,0.66,ak,ak022txqam5,2022-01-19T10:51:33.803Z,"35 km SE of Denali National Park, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-18T10:04:33.682Z,60.4096,-147.4265,12.8,1.6,ml,,,,0.89,ak,ak022txnien,2022-01-18T10:18:05.322Z,"50 km NE of Chenega, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T10:02:41.430Z,32.9411667,-115.8313333,8.29,1.69,ml,51,32,0.0148,0.25,ci,ci39915415,2022-01-18T20:43:04.110Z,"22km WSW of Westmorland, CA",earthquake,0.23,0.49,0.234,22,reviewed,ci,ci
2022-01-18T10:00:06.090Z,38.8223343,-122.8548355,2.55,0.36,md,15,67,0.005441,0.02,nc,nc73680131,2022-01-18T10:01:44.634Z,"10km WNW of The Geysers, CA",earthquake,0.27,0.6,0.21,3,automatic,nc,nc
2022-01-18T09:59:55.170Z,17.8213,-67.0336,10,3.01,md,20,263,0.1485,0.13,pr,pr2022018008,2022-01-18T11:38:30.347Z,"17 km S of La Parguera, Puerto Rico",earthquake,0.57,0.5,0.16,7,reviewed,pr,pr
2022-01-18T09:34:52.056Z,31.72577046,-104.4982398,3.997802734,2.3,ml,21,86,0.03057219044,0.2,tx,tx2022bfuo,2022-01-18T09:58:40.237Z,"51 km SSW of Whites City, New Mexico",earthquake,2.673787597,1.775447921,0.1,13,reviewed,tx,tx
2022-01-18T09:15:31.390Z,37.5516667,-118.8188333,6.19,0.66,md,16,238,0.03915,0.04,nc,nc73680126,2022-01-18T18:42:02.226Z,"12km W of Toms Place, CA",earthquake,0.93,1.16,0.137,15,reviewed,nc,nc
2022-01-18T09:11:37.760Z,60.4109,-147.8287,20,1.5,ml,,,,0.38,ak,ak022tx3l4g,2022-01-18T09:15:36.709Z,"39 km NNE of Chenega, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-18T09:03:39.160Z,38.5911667,-122.7538333,6.34,1.22,md,33,83,0.1194,0.07,nc,nc73680121,2022-01-18T20:32:11.071Z,"7km NE of Windsor, CA",earthquake,0.22,1.11,0.23,20,reviewed,nc,nc
2022-01-18T09:02:47.204Z,-17.5516,-70.4314,97.6,4.1,mb,,142,0.819,1.03,us,us7000gcue,2022-01-18T09:44:35.040Z,"16 km SSE of Ilabaya, Peru",earthquake,6.9,2.6,0.135,15,reviewed,us,us
2022-01-18T08:56:52.940Z,33.826,-116.7383333,13.09,0.47,ml,17,213,0.04972,0.06,ci,ci39915399,2022-01-18T20:24:30.529Z,"10km N of Idyllwild, CA",earthquake,0.44,0.31,0.155,7,reviewed,ci,ci
2022-01-18T08:56:42.615Z,58.1012,-151.5995,45.9,3.6,ml,,,,1.02,ak,ak022twrstt,2022-01-18T19:33:35.393Z,"56 km ENE of Ouzinkie, Alaska",earthquake,,0.7,,,reviewed,ak,ak
2022-01-18T08:54:50.550Z,35.9521667,-117.6768333,5.51,0.65,ml,13,100,0.02188,0.1,ci,ci39915391,2022-01-18T14:32:00.955Z,"21km E of Little Lake, CA",earthquake,0.34,0.52,0.156,5,reviewed,ci,ci
2022-01-18T08:53:34.511Z,61.7645,-147.1624,22.8,1.1,ml,,,,0.52,ak,ak022twr5dh,2022-01-18T08:59:13.941Z,"19 km S of Eureka Roadhouse, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-18T08:52:34.370Z,35.8235,-117.6381667,10.11,0.74,ml,8,112,0.03394,0.1,ci,ci39915383,2022-01-18T14:32:00.686Z,"22km WNW of Searles Valley, CA",earthquake,0.44,0.62,0.154,8,reviewed,ci,ci
2022-01-18T08:48:56.656Z,61.1598,-140.5215,16.4,1.2,ml,,,,0.8,ak,ak022twq4gx,2022-01-18T08:51:52.777Z,"132 km ESE of McCarthy, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T08:45:54.680Z,19.175666809082,-155.468505859375,31.6399993896484,2.17,ml,44,98,,0.109999999,hv,hv72879687,2022-01-18T08:51:25.660Z,"3 km SSE of Pāhala, Hawaii",earthquake,0.44,0.660000026,3.67,6,automatic,hv,hv
2022-01-18T08:44:37.210Z,33.8278333,-116.7495,12.51,2.44,ml,101,19,0.04026,0.15,ci,ci39915375,2022-01-18T20:21:52.380Z,"10km NNW of Idyllwild, CA",earthquake,0.1,0.26,0.179,26,reviewed,ci,ci
2022-01-18T08:39:57.848Z,59.7186,-150.8046,37.5,1.8,ml,,,,0.65,ak,ak022two748,2022-01-18T08:43:11.718Z,"17 km SSE of Fox River, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-18T08:27:06.160Z,33.8306667,-116.7426667,11.38,1.07,ml,51,43,0.04563,0.17,ci,ci39915367,2022-01-18T22:12:40.598Z,"10km NNW of Idyllwild, CA",earthquake,0.19,0.45,0.203,26,reviewed,ci,ci
2022-01-18T08:18:35.820Z,33.822,-116.7393333,12.45,0.3,ml,16,207,0.04968,0.08,ci,ci39915351,2022-01-18T20:06:22.430Z,"9km NNW of Idyllwild, CA",earthquake,0.49,0.41,0.101,8,reviewed,ci,ci
2022-01-18T08:13:45.260Z,33.8303333,-116.7401667,11.72,1.23,ml,50,42,0.04773,0.19,ci,ci39915343,2022-01-18T14:33:39.098Z,"10km N of Idyllwild, CA",earthquake,0.21,0.49,0.163,27,reviewed,ci,ci
2022-01-18T08:12:50.110Z,38.747,-122.7258333,1.06,0.21,md,19,165,0.0128,0.05,nc,nc73680111,2022-01-18T23:48:30.095Z,"4km SW of Anderson Springs, CA",earthquake,0.24,0.16,0.067,4,reviewed,nc,nc
2022-01-18T08:10:57.970Z,33.8313333,-116.7411667,11.8,1.01,ml,42,53,0.04684,0.17,ci,ci39915335,2022-01-18T14:33:41.760Z,"10km NNW of Idyllwild, CA",earthquake,0.21,0.45,0.17,28,reviewed,ci,ci
2022-01-18T08:08:41.130Z,33.0986667,-116.259,11.12,1.23,ml,57,40,0.09386,0.19,ci,ci39915327,2022-01-18T20:03:26.414Z,"13km WSW of Ocotillo Wells, CA",earthquake,0.18,0.38,0.145,30,reviewed,ci,ci
2022-01-18T08:03:55.570Z,34.458,-119.2991667,3.21,1.48,ml,38,50,0.06088,0.24,ci,ci39915319,2022-01-18T19:56:37.310Z,"5km WNW of Ojai, CA",earthquake,0.24,0.55,0.147,25,reviewed,ci,ci
2022-01-18T07:59:09.493Z,-20.4401,-175.3281,10,4.6,mb,,188,6.808,0.61,us,us7000ge4x,2022-01-22T04:00:04.040Z,"78 km N of Nuku‘alofa, Tonga",earthquake,10.7,2,0.157,12,reviewed,us,us
2022-01-18T07:58:24.280Z,33.8245,-116.7398333,13.56,0.63,ml,28,48,0.04875,0.11,ci,ci39915311,2022-01-18T18:39:50.594Z,"10km NNW of Idyllwild, CA",earthquake,0.15,0.37,0.151,12,reviewed,ci,ci
2022-01-18T07:42:14.890Z,34.5746667,-119.4631667,1.17,1.52,ml,24,55,0.1646,0.17,ci,ci39915303,2022-01-18T19:50:33.700Z,"20km NNE of Carpinteria, CA",earthquake,0.23,0.55,0.115,15,reviewed,ci,ci
2022-01-18T07:41:41.981Z,57.9527,-156.4325,129.9,1.8,ml,,,,0.16,ak,ak022tw35vr,2022-01-18T19:13:13.896Z,"62 km ESE of Egegik, Alaska",earthquake,,0.8,,,reviewed,ak,ak
2022-01-18T07:41:40.640Z,33.3771667,-116.867,6.71,0.58,ml,21,72,0.02377,0.17,ci,ci37379508,2022-01-18T19:40:52.230Z,"2km N of Palomar Observatory, CA",earthquake,0.35,0.49,0.1,12,reviewed,ci,ci
2022-01-18T07:41:28.080Z,33.8311667,-116.7413333,12.87,1.21,ml,37,48,0.04671,0.11,ci,ci39915295,2022-01-18T19:36:34.723Z,"10km NNW of Idyllwild, CA",earthquake,0.17,0.35,0.122,9,reviewed,ci,ci
2022-01-18T07:39:15.120Z,33.8255,-116.7506667,12.48,3.45,mw,145,19,0.03971,0.2,ci,ci39915287,2022-01-22T11:52:59.360Z,"10km NNW of Idyllwild, CA",earthquake,0.11,0.26,,4,reviewed,ci,ci
2022-01-18T07:38:27.190Z,33.4805,-116.4605,9.45,0.45,ml,26,69,0.05173,0.14,ci,ci39915279,2022-01-18T19:29:37.144Z,"21km ESE of Anza, CA",earthquake,0.21,0.58,0.22,14,reviewed,ci,ci
2022-01-18T07:30:36.270Z,35.8776667,-117.7071667,10.89,1.13,ml,26,37,0.08339,0.08,ci,ci39915271,2022-01-18T19:26:06.460Z,"19km ESE of Little Lake, CA",earthquake,0.13,0.23,0.179,13,reviewed,ci,ci
2022-01-18T07:30:05.230Z,19.6731,-63.7595,82,3.81,md,7,341,2.0455,0.24,pr,pr2022018007,2022-01-18T07:51:25.337Z,"177 km NNW of The Valley, Anguilla",earthquake,5.29,14.06,0.08,5,reviewed,pr,pr
2022-01-18T07:25:27.020Z,46.9295,-112.531,10.84,0.89,ml,11,82,0.087,0.11,mb,mb80536299,2022-01-18T19:04:38.340Z,"11 km ESE of Lincoln, Montana",earthquake,0.39,0.63,0.125,4,reviewed,mb,mb
2022-01-18T07:25:13.310Z,19.2048,-67.2103,13,3.47,md,10,258,0.7439,0.24,pr,pr2022018006,2022-01-18T07:49:14.777Z,"79 km N of San Antonio, Puerto Rico",earthquake,2.47,3.59,0.04,3,reviewed,pr,pr
2022-01-18T07:23:14.850Z,46.2008333333333,-122.186333333333,4.16,1.38,ml,22,69,0.0008581,0.15,uw,uw61802387,2022-01-18T18:44:51.630Z,"38 km NNE of Amboy, Washington",earthquake,0.37,0.33,0.148022831278485,9,reviewed,uw,uw
2022-01-18T07:21:20.037Z,38.1503,-117.9017,9.1,1,ml,12,150.87,0.047,0.1001,nn,nn00831859,2022-01-19T02:37:45.419Z,"32 km SE of Mina, Nevada",earthquake,,1.4,0.59,4,reviewed,nn,nn
2022-01-18T07:20:02.830Z,19.2338333129883,-155.42333984375,32.8600006103516,1.99000001,md,42,127,,0.119999997,hv,hv72879602,2022-01-18T07:23:18.410Z,"6 km ENE of Pāhala, Hawaii",earthquake,0.54,0.730000019,0.660000026,11,automatic,hv,hv
2022-01-18T07:19:25.534Z,36.648,-116.2789,6.9,0,ml,8,195.29,0.048,0.1196,nn,nn00831882,2022-01-19T02:38:04.445Z,"51 km SE of Beatty, Nevada",earthquake,,2.5,0.13,3,reviewed,nn,nn
2022-01-18T07:18:46.667Z,39.2814,-120.0148,6.7,-0.1,ml,6,113.54,0.02,0.1223,nn,nn00831908,2022-01-19T02:38:18.982Z,"4 km NW of Incline Village, Nevada",earthquake,,1.9,0.17,3,reviewed,nn,nn
2022-01-18T07:13:42.360Z,38.8486671,-122.8186646,1.26,0.37,md,12,94,0.007014,0.02,nc,nc73680086,2022-01-18T07:15:18.547Z,"9km WNW of Cobb, CA",earthquake,0.28,0.66,,1,automatic,nc,nc
2022-01-18T07:12:32.600Z,35.563,-120.7971667,5.13,2.26,md,53,49,0.06152,0.1,nc,nc73680091,2022-01-22T02:01:11.211Z,"8km W of Templeton, CA",earthquake,0.16,0.36,0.171,52,reviewed,nc,nc
2022-01-18T06:54:00.570Z,37.4471667,-119.2721667,16.54,1.1,md,17,133,0.1023,0.04,nc,nc73680076,2022-01-18T08:31:12.836Z,"32km NE of North Fork, CA",earthquake,0.65,1.14,0.236,16,reviewed,nc,nc
2022-01-18T06:52:35.057Z,-20.7433,-175.4879,10,4.7,mb,,124,6.791,0.69,us,us7000gcty,2022-01-22T03:29:13.040Z,"52 km NW of Nuku‘alofa, Tonga",earthquake,15.8,1.9,0.094,34,reviewed,us,us
2022-01-18T06:51:52.070Z,17.9678,-66.8413,11,2.02,md,10,185,0.0386,0.12,pr,pr2022018005,2022-01-18T07:04:27.764Z,"3 km SW of Indios, Puerto Rico",earthquake,0.42,0.59,0.17,9,reviewed,pr,pr
2022-01-18T06:49:20.120Z,39.4241667,-110.3083333,-2.03,1.66,ml,10,181,0.01299,0.14,uu,uu60477922,2022-01-18T17:46:29.610Z,"15 km SSE of Sunnyside, Utah",earthquake,1,1.11,0.13,3,reviewed,uu,uu
2022-01-18T06:43:07.142Z,63.0822,-150.6258,114.8,1.4,ml,,,,0.25,ak,ak022tvi2uy,2022-01-18T06:46:28.455Z,"65 km N of Petersville, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-18T06:36:24.718Z,61.887,-149.9339,42.5,1.4,ml,,,,0.46,ak,ak022tvgm79,2022-01-18T07:46:55.504Z,"16 km NNE of Willow, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-18T06:33:57.270Z,38.8608322,-122.8518295,0.72,0.53,md,15,158,0.01877,0.06,nc,nc73680071,2022-01-18T06:35:31.886Z,"12km WNW of Cobb, CA",earthquake,0.37,0.58,0.23,2,automatic,nc,nc
2022-01-18T06:31:44.856Z,58.8903,-150.5857,42.4,2,ml,,,,0.51,ak,ak022tvfl6z,2022-01-18T06:37:06.909Z,"86 km SSE of Halibut Cove, Alaska",earthquake,,3,,,automatic,ak,ak
2022-01-18T06:24:45.320Z,34.4753333,-118.0115,9.09,0.39,ml,10,68,0.0533,0.07,ci,ci39915247,2022-01-18T19:21:05.269Z,"6km SSW of Littlerock, CA",earthquake,0.2,0.35,0.107,6,reviewed,ci,ci
2022-01-18T06:18:35.090Z,44.5396667,-115.2508333,7.69,2.35,ml,15,82,0.765,0.27,mb,mb80536249,2022-01-18T16:10:08.870Z,"43 km NW of Stanley, Idaho",earthquake,0.66,1.37,0.193,14,reviewed,mb,mb
2022-01-18T06:16:26.524Z,31.09451513,-103.3344648,5.668823242,2.4,ml,31,49,0.07703415052,0.3,tx,tx2022bfnz,2022-01-19T23:04:45.591Z,"30 km WSW of Coyanosa, Texas",earthquake,0.908050374,1.318111433,0.1,16,reviewed,tx,tx
2022-01-18T06:13:47.571Z,38.5411,-119.4934,6.6,1.4,ml,17,111.95,0.05,0.1718,nn,nn00831858,2022-01-19T02:37:44.502Z,"3 km SSE of Coleville, California",earthquake,,1.1,0.24,3,reviewed,nn,nn
2022-01-18T06:10:09.500Z,33.4438333,-116.5808333,11.61,0.96,ml,49,43,0.05467,0.16,ci,ci39915239,2022-01-18T19:21:00.880Z,"15km SE of Anza, CA",earthquake,0.15,0.38,0.134,28,reviewed,ci,ci
2022-01-18T06:05:45.530Z,53.6861666666667,-166.822333333333,6.08,0.52,ml,9,293,,0.15,av,av91047378,2022-01-20T02:10:59.680Z,"28 km SW of Unalaska, Alaska",earthquake,0.75,0.51,0.253999999097465,9,reviewed,av,av
2022-01-18T05:52:18.140Z,38.8376656,-122.87883,1.38,1.22,md,19,89,0.003653,0.08,nc,nc73680061,2022-01-18T06:10:10.892Z,"12km ENE of Cloverdale, CA",earthquake,0.63,0.76,0.05,3,automatic,nc,nc
2022-01-18T05:51:31.930Z,38.8370018,-122.8785019,3,0.35,md,9,78,0.004054,0.01,nc,nc73680056,2022-01-18T05:53:06.520Z,"12km WNW of The Geysers, CA",earthquake,0.37,0.8,0.04,3,automatic,nc,nc
2022-01-18T05:50:09.554Z,39.4353,-119.8245,9.1,0.1,ml,4,167.46,0.194,0.1078,nn,nn00831906,2022-01-19T02:38:18.061Z,"10 km S of Reno, Nevada",earthquake,,7,0.61,3,reviewed,nn,nn
2022-01-18T05:49:14.727Z,36.6519,-116.2787,7.5,-0.2,ml,9,189.36,0.049,0.0714,nn,nn00831883,2022-01-19T02:38:05.174Z,"51 km ESE of Beatty, Nevada",earthquake,,1.8,0.06,3,reviewed,nn,nn
2022-01-18T05:47:46.950Z,34.85616667,-97.81883333,6.57,1.18,ml,26,53,0.08728287212,0.48,ok,ok2022bfna,2022-01-19T14:08:16.958Z,"7 km SSW of Alex, Oklahoma",earthquake,,1.5,0.17,16,reviewed,ok,ok
2022-01-18T05:46:27.316Z,61.2564,-146.829,16.1,1.8,ml,,,,0.63,ak,ak022tuxbyj,2022-01-18T05:51:11.394Z,"29 km WNW of Valdez, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T05:44:39.300Z,38.8460007,-122.8160019,0.39,0.86,md,10,82,0.01038,0.03,nc,nc73680051,2022-01-18T05:46:17.124Z,"8km WNW of Cobb, CA",earthquake,0.29,0.66,,1,automatic,nc,nc
2022-01-18T05:43:01.160Z,18.5511,-68.3346,52,3.57,md,13,223,1.2262,0.33,pr,pr2022018004,2022-01-18T06:14:08.168Z,"8 km ESE of Punta Cana, Dominican Republic",earthquake,3.36,4.6,0.15,4,reviewed,pr,pr
2022-01-18T05:32:46.560Z,38.7815018,-122.7243347,1.57,0.7,md,12,80,0.009838,0.02,nc,nc73680046,2022-01-18T05:34:21.900Z,"3km E of The Geysers, CA",earthquake,0.28,0.95,0.17,2,automatic,nc,nc
2022-01-18T05:26:42.420Z,38.8243333,-122.8006667,4.18,0.59,md,4,128,0.007408,0,nc,nc73680041,2022-01-21T23:04:31.051Z,"6km NW of The Geysers, CA",earthquake,1.76,7.42,,1,reviewed,nc,nc
2022-01-18T05:26:27.469Z,0.9958,124.3034,217.99,4.5,mb,,66,2.538,0.77,us,us7000gct1,2022-01-18T07:03:44.040Z,"66 km WSW of Tomohon, Indonesia",earthquake,6.3,7.7,0.084,42,reviewed,us,us
2022-01-18T05:25:32.780Z,36.0561676,-120.6409988,-0.72,1.99,md,24,109,0.03844,0.18,nc,nc73680036,2022-01-18T06:44:11.219Z,"24km E of San Ardo, CA",earthquake,0.42,3.11,0.1,14,automatic,nc,nc
2022-01-18T05:25:12.060Z,33.5421667,-118.1601667,2.91,1.99,ml,33,95,0.1915,0.24,ci,ci39915207,2022-01-18T18:32:18.050Z,"22km SW of Huntington Beach, CA",earthquake,0.39,2.3,0.169,51,reviewed,ci,ci
2022-01-18T05:24:10.600Z,36.1033333,-89.7578333,8.15,2.47,md,50,59,0.04817,0.09,nm,nm60379596,2022-01-19T04:04:30.577Z,"6 km ENE of Steele, Missouri",earthquake,0.12,0.35,0.09,44,reviewed,nm,nm
2022-01-18T05:19:25.830Z,32.9213333,-116.2281667,8.84,0.61,ml,20,102,0.07142,0.15,ci,ci39915199,2022-01-18T19:10:19.357Z,"26km SSW of Ocotillo Wells, CA",earthquake,0.32,0.62,0.158,8,reviewed,ci,ci
2022-01-18T05:18:59.647Z,-20.4725,-175.249,10,4.4,mb,,149,6.889,0.53,us,us7000ge4u,2022-01-22T03:39:28.040Z,"73 km N of Nuku‘alofa, Tonga",earthquake,15.9,1.8,0.269,4,reviewed,us,us
2022-01-18T05:12:37.923Z,36.6459,-116.2735,7,0,ml,8,199.16,0.053,0.0867,nn,nn00831878,2022-01-19T02:38:01.679Z,"52 km SE of Beatty, Nevada",earthquake,,2.3,0.11,2,reviewed,nn,nn
2022-01-18T04:57:49.525Z,47.3048,142.4527,10,4.5,mb,,96,0.405,0.47,us,us7000gcss,2022-01-21T02:25:41.040Z,"8 km WSW of Bykov, Russia",earthquake,4.4,1.9,0.073,55,reviewed,us,us
2022-01-18T04:56:23.246Z,61.6748,-151.326,10,0.8,ml,,,,0.71,ak,ak022tue178,2022-01-18T05:00:15.496Z,"35 km S of Skwentna, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-18T04:53:24.630Z,38.8263321,-122.8050003,2.11,0.35,md,8,75,0.00493,0.02,nc,nc73680031,2022-01-18T04:55:02.606Z,"7km NW of The Geysers, CA",earthquake,0.45,1.29,,1,automatic,nc,nc
2022-01-18T04:51:55.150Z,35.9916667,-117.4156667,1.69,1.63,ml,33,62,0.1471,0.13,ci,ci39915191,2022-01-18T19:07:30.927Z,"25km N of Searles Valley, CA",earthquake,0.2,0.38,0.136,19,reviewed,ci,ci
2022-01-18T04:41:35.160Z,60.5203333333333,-152.810333333333,4.27,-0.57,ml,7,100,,0.05,av,av91465891,2022-01-20T02:01:41.520Z,"82 km NW of Ninilchik, Alaska",earthquake,0.29,0.72,0.20621398573655,7,reviewed,av,av
2022-01-18T04:33:27.266Z,-26.4499,27.3034,10,4.4,mb,,120,2.1,0.71,us,us7000gcsp,2022-01-21T01:21:56.040Z,"13 km SW of Carletonville, South Africa",earthquake,9.7,1.9,0.203,7,reviewed,us,us
2022-01-18T04:31:14.123Z,60.938,-149.5741,28.8,1.6,ml,,,,0.62,ak,ak022tu8nlf,2022-01-18T04:36:02.719Z,"4 km ENE of Hope, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T04:23:57.270Z,62.3562,-149.0565,14.5,1.3,ml,,,,0.59,ak,ak022tu7173,2022-01-18T04:26:41.298Z,"46 km ENE of Susitna North, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T04:21:31.394Z,36.6547,-116.2798,7.5,-0.2,ml,7,184.72,0.048,0.0661,nn,nn00831877,2022-01-19T02:38:00.752Z,"51 km ESE of Beatty, Nevada",earthquake,,2,0.02,2,reviewed,nn,nn
2022-01-18T04:12:49.360Z,38.8168335,-122.7959976,2.49,0.64,md,18,49,0.008869,0.03,nc,nc73680011,2022-01-18T04:14:26.551Z,"6km NW of The Geysers, CA",earthquake,0.26,0.57,0.15,3,automatic,nc,nc
2022-01-18T04:08:08.770Z,33.5441667,-116.706,2.44,0.14,ml,10,185,0.03364,0.09,ci,ci37379500,2022-01-18T18:35:08.608Z,"3km WSW of Anza, CA",earthquake,0.4,0.29,0.216,2,reviewed,ci,ci
2022-01-18T04:07:35.650Z,33.6098333,-116.4528333,16.99,0.06,ml,3,325,0.003422,0.05,ci,ci39915183,2022-01-18T18:30:16.817Z,"14km SSW of Palm Desert, CA",earthquake,5.66,0.54,0.147,1,reviewed,ci,ci
2022-01-18T04:02:16.430Z,38.8160019,-122.8125,1.3,0.84,md,10,211,0.007622,0.02,nc,nc73680006,2022-01-18T04:03:52.677Z,"6km NW of The Geysers, CA",earthquake,0.7,0.93,,1,automatic,nc,nc
2022-01-18T03:56:22.820Z,34.5106667,-120.6706667,-0.05,2.65,ml,31,203,0.2576,0.19,ci,ci39915175,2022-01-21T00:22:21.040Z,"24km SW of Lompoc, CA",earthquake,0.53,0.74,0.119,26,reviewed,ci,ci
2022-01-18T03:43:23.720Z,38.7901649,-122.7666702,1.54,0.55,md,11,86,0.01178,0.03,nc,nc73679991,2022-01-18T03:45:01.926Z,"2km NNW of The Geysers, CA",earthquake,0.29,0.57,0.3,3,automatic,nc,nc
2022-01-18T03:41:51.125Z,37.528,-116.3735,6.8,0.5,ml,7,301.89,0.36,0.1816,nn,nn00831890,2022-01-19T02:38:08.596Z,"57 km WSW of Rachel, Nevada",earthquake,,8.6,1.22,4,reviewed,nn,nn
2022-01-18T03:39:54.025Z,63.8679,-145.5298,9.2,1.2,ml,,,,0.79,ak,ak022ttp0sp,2022-01-18T03:50:27.349Z,"8 km SSE of Fort Greely, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T03:33:10.473Z,59.2399,-154.623,4.3,1.2,ml,,,,0.85,ak,ak022ttnn64,2022-01-18T18:58:21.704Z,"23 km SSE of Kokhanok, Alaska",earthquake,,0.8,,,reviewed,ak,ak
2022-01-18T03:30:58.090Z,17.9838,-66.7998,15,2.23,md,11,192,0.0799,0.07,pr,pr2022018003,2022-01-18T03:44:46.882Z,"2 km ESE of Indios, Puerto Rico",earthquake,0.64,0.39,0.14,9,reviewed,pr,pr
2022-01-18T03:24:57.970Z,17.9601,-66.9276,13,2.39,md,15,190,0.0507,0.16,pr,pr2022018002,2022-01-18T03:39:39.100Z,"2 km WSW of Guánica, Puerto Rico",earthquake,0.59,0.27,0.09,9,reviewed,pr,pr
2022-01-18T03:20:29.274Z,6.0273,126.3354,103.14,4.5,mb,,123,1.279,0.95,us,us7000gcsb,2022-01-21T02:10:33.040Z,"40 km SSE of Pondaguitan, Philippines",earthquake,7.7,5.9,0.132,17,reviewed,us,us
2022-01-18T03:20:14.110Z,45.8785,-111.2898333,13.53,1.11,ml,5,308,0.369,0.07,mb,mb80536324,2022-01-18T20:50:14.010Z,"4 km NE of Manhattan, Montana",earthquake,1.96,0.84,0.129,3,reviewed,mb,mb
2022-01-18T03:15:19.040Z,33.9496667,-116.3853333,9.78,0.79,ml,30,80,0.02144,0.11,ci,ci39915159,2022-01-18T18:58:48.032Z,"11km E of Desert Hot Springs, CA",earthquake,0.21,0.31,0.143,19,reviewed,ci,ci
2022-01-18T03:11:01.848Z,61.9947,-150.6146,69.6,1.2,ml,,,,0.67,ak,ak022ttiwst,2022-01-18T03:36:44.771Z,"41 km NW of Willow, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-18T03:09:02.697Z,15.4508,-95.6013,10,4.6,mb,,86,3.434,0.72,us,us7000gcsa,2022-01-21T02:03:26.531Z,"56 km SSE of El Coyul, Mexico",earthquake,8.1,1.9,0.044,154,reviewed,us,us
2022-01-18T03:08:51.794Z,61.5462,-148.3938,27.6,1.3,ml,,,,0.81,ak,ak022tticwl,2022-01-18T03:20:22.639Z,"28 km S of Chickaloon, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-18T03:03:15.680Z,36.7358322,-121.4111633,6.43,1.76,md,19,145,0.04038,0.14,nc,nc73679981,2022-01-18T03:37:11.032Z,"9km SSW of Ridgemark, CA",earthquake,0.44,0.79,0.21,11,automatic,nc,nc
2022-01-18T03:01:20.508Z,-24.0884,-67.1888,226.87,4.4,mb,,72,1.451,0.51,us,us7000gcs6,2022-01-21T01:37:43.040Z,"89 km W of San Antonio de los Cobres, Argentina",earthquake,7.8,2.9,0.162,11,reviewed,us,us
2022-01-18T02:49:38.690Z,38.8426666,-122.8255005,1.51,0.37,md,8,101,0.008798,0.02,nc,nc73679976,2022-01-18T02:51:15.664Z,"9km WNW of Cobb, CA",earthquake,0.47,0.87,,1,automatic,nc,nc
2022-01-18T02:48:51.700Z,39.42,-110.2873333,-3.38,1.89,ml,13,203,0.02954,0.19,uu,uu60477917,2022-01-18T14:22:58.980Z,"16 km SSE of Sunnyside, Utah",earthquake,1.12,2.62,0.109,3,reviewed,uu,uu
2022-01-18T02:41:14.856Z,63.5198,-147.4118,0,1.5,ml,,,,0.49,ak,ak022tt3xmq,2022-01-18T03:10:51.123Z,"78 km E of Cantwell, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-18T02:25:16.720Z,60.1803,-140.9127,20.2,1.4,ml,,,,1.28,ak,ak022tt0iag,2022-01-18T02:29:15.911Z,"Southern Yukon Territory, Canada",earthquake,,0.4,,,automatic,ak,ak
2022-01-18T02:22:16.154Z,24.0926,93.6186,59.74,4.4,mb,,81,4.574,0.57,us,us7000gcs1,2022-01-20T22:46:27.040Z,"27 km S of Churāchāndpur, India",earthquake,8,8.9,0.108,25,reviewed,us,us
2022-01-18T02:14:32.320Z,35.9125,-117.7153333,2.73,1.49,ml,27,42,0.06346,0.11,ci,ci39915135,2022-01-18T18:55:42.170Z,"17km E of Little Lake, CA",earthquake,0.13,0.26,0.212,20,reviewed,ci,ci
2022-01-18T02:13:34.430Z,38.7938333,-122.7886667,0.21,0.13,md,11,100,0.000877,0.02,nc,nc73679966,2022-01-20T21:56:17.510Z,"3km WNW of The Geysers, CA",earthquake,0.26,0.35,0.325,2,reviewed,nc,nc
2022-01-18T02:11:23.320Z,33.9941667,-117.5338333,2.66,1.02,ml,28,62,0.02532,0.14,ci,ci39915127,2022-01-18T18:52:29.218Z,"2km W of Mira Loma, CA",earthquake,0.2,0.23,0.216,19,reviewed,ci,ci
2022-01-18T01:57:28.604Z,61.9816,-149.4431,44.1,1.4,ml,,,,0.69,ak,ak022tslyid,2022-01-18T02:01:32.597Z,"28 km NNW of Fishhook, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-18T01:52:59.730Z,34.1456667,-117.435,7.8,0.84,ml,26,82,0.04609,0.14,ci,ci39915119,2022-01-18T18:47:37.777Z,"6km NNE of Fontana, CA",earthquake,0.32,0.56,0.139,15,reviewed,ci,ci
2022-01-18T01:49:07.020Z,19.1696662902832,-155.421829223633,33.6800003051758,1.73000002,md,39,164,,0.0900000036,hv,hv72879192,2022-01-18T01:52:08.340Z,"Island of Hawaii, Hawaii",earthquake,0.57,0.790000021,0.129999995,5,automatic,hv,hv
2022-01-18T01:48:53.960Z,38.8330002,-122.8156662,1.88,0.85,md,11,73,0.01054,0.02,nc,nc73679961,2022-01-18T01:50:32.196Z,"8km NW of The Geysers, CA",earthquake,0.33,0.74,,1,automatic,nc,nc
2022-01-18T01:45:24.370Z,37.1908333,-112.8736667,21.24,1.48,ml,9,172,0.1787,0.09,uu,uu60477912,2022-01-18T14:26:06.450Z,"11 km E of Springdale, Utah",earthquake,0.55,0.93,0.4,4,reviewed,uu,uu
2022-01-18T01:41:55.220Z,36.4025,-117.8319,0,1.8,ml,7,102.94,0.204,0.1849,nn,nn00831887,2022-01-19T02:38:07.477Z,"10 km SSE of Keeler, California",earthquake,,0,0.61,2,reviewed,nn,nn
2022-01-18T01:39:22.390Z,44.9846667,-113.0305,3.66,1.99,ml,13,164,0.203,0.14,mb,mb80536244,2022-01-18T15:34:56.610Z,"40 km SW of Dillon, Montana",earthquake,0.62,2.19,0.153,10,reviewed,mb,mb
2022-01-18T01:35:46.570Z,40.3575,-126.7827,10,2.4,ml,,284,1.866,0.56,us,us7000gcu3,2022-01-20T21:59:39.040Z,"214 km W of Ferndale, California",earthquake,4.7,2,0.077,22,reviewed,us,us
2022-01-18T01:24:32.792Z,62.0481,-150.2962,16.2,1.2,ml,,,,0.37,ak,ak022tsew7q,2022-01-18T01:30:38.948Z,"26 km WSW of Susitna North, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-18T01:12:54.160Z,38.7921677,-122.7884979,0.24,0.35,md,5,121,0.001107,0.01,nc,nc73679951,2022-01-18T01:14:31.889Z,"3km WNW of The Geysers, CA",earthquake,0.4,0.56,,1,automatic,nc,nc
2022-01-18T01:05:30.410Z,38.8266667,-122.8521667,2.22,-0.14,md,11,88,0.003779,0.02,nc,nc73679946,2022-01-21T23:03:00.526Z,"10km WNW of The Geysers, CA",earthquake,0.54,0.59,,1,reviewed,nc,nc
2022-01-18T01:03:19.910Z,19.2748,-67.812,35,3.54,md,18,262,0.9503,0.58,pr,pr2022018001,2022-01-20T21:51:53.040Z,"98 km NE of Punta Cana, Dominican Republic",earthquake,4.16,27.8,0.09,16,reviewed,pr,pr
2022-01-18T00:59:17.880Z,38.8273315,-122.8544998,2.23,0.77,md,21,61,0.001866,0.03,nc,nc73679941,2022-01-18T01:00:53.123Z,"10km WNW of The Geysers, CA",earthquake,0.23,0.46,0.12,4,automatic,nc,nc
2022-01-18T00:58:49.610Z,19.1749992370605,-155.479995727539,35.8800010681152,2.25,md,42,79,,0.119999997,hv,hv72879157,2022-01-18T01:02:02.810Z,"3 km S of Pāhala, Hawaii",earthquake,0.5,0.730000019,1.23000002,15,automatic,hv,hv
2022-01-18T00:55:02.896Z,43.8673,148.0219,35,4.3,mb,,185,3.925,0.62,us,us7000gcrq,2022-01-18T01:19:44.040Z,"104 km E of Shikotan, Russia",earthquake,11.1,2,0.099,29,reviewed,us,us
2022-01-18T00:52:29.039Z,36.777,-98.31983333,4.6,1.5,ml,77,126,0.2996412002,0.25,ok,ok2022bfdh,2022-01-19T14:00:46.601Z,"4 km NE of Cherokee, Oklahoma",earthquake,,0.6,0.2,30,reviewed,ok,ok
2022-01-18T00:52:06.960Z,33.9923333,-117.1588333,10.59,0.58,ml,21,117,0.136,0.14,ci,ci39915103,2022-01-18T18:43:27.112Z,"7km SSE of Redlands, CA",earthquake,0.25,0.71,0.084,10,reviewed,ci,ci
2022-01-18T00:46:03.595Z,-7.7677,127.8492,187.43,4.5,mb,,71,3.424,1.42,us,us7000gcrl,2022-01-18T01:09:02.040Z,"125 km NE of Lospalos, Timor Leste",earthquake,9.2,9.7,0.108,25,reviewed,us,us
2022-01-18T00:45:02.550Z,40.6958333,-112.1,11.69,0.78,md,11,73,0.01596,0.1,uu,uu60477907,2022-01-18T16:58:30.220Z,"1 km S of Magna, Utah",earthquake,0.42,0.7,0.238,8,reviewed,uu,uu
2022-01-18T00:41:50.020Z,38.8153343,-122.8206635,2.55,0.9,md,19,52,0.00927,0.02,nc,nc73679936,2022-01-18T00:43:25.917Z,"7km NW of The Geysers, CA",earthquake,0.24,0.55,0.2,4,automatic,nc,nc
2022-01-18T00:35:45.527Z,61.1979,-150.6384,28.6,0.7,ml,,,,0.59,ak,ak022trvthd,2022-01-18T18:45:39.992Z,"24 km ENE of Beluga, Alaska",earthquake,,14.1,,,reviewed,ak,ak
2022-01-18T00:34:48.870Z,38.7939987,-122.7898331,0.02,0.14,md,12,101,0.001706,0.04,nc,nc73679926,2022-01-18T00:36:27.472Z,"3km WNW of The Geysers, CA",earthquake,0.23,0.47,0.07,3,automatic,nc,nc
2022-01-18T00:34:31.210Z,37.4958333,-118.8673333,4.03,0.35,md,10,228,0.09882,0.1,nc,nc73679931,2022-01-18T00:57:01.790Z,"18km WSW of Toms Place, CA",earthquake,0.92,2.12,0.125,8,reviewed,nc,nc
2022-01-18T00:33:00.280Z,47.4158333333333,-122.7155,28.77,1.35,ml,24,59,0.05065,0.27,uw,uw61802367,2022-01-18T19:20:38.620Z,"6 km W of Burley, Washington",earthquake,0.5,1.2,0.113849126256442,8,reviewed,uw,uw
2022-01-18T00:29:21.815Z,38.1809,-117.8124,7.2,1.5,ml,18,117.16,0.123,0.153,nn,nn00831855,2022-01-19T02:37:40.301Z,"34 km SE of Mina, Nevada",earthquake,,2.1,0.54,5,reviewed,nn,nn
2022-01-18T00:27:57.868Z,38.1624,-117.8942,9.5,1.2,ml,14,157.44,0.057,0.0963,nn,nn00831853,2022-01-19T02:37:37.615Z,"31 km SE of Mina, Nevada",earthquake,,1.4,0.26,4,reviewed,nn,nn
2022-01-18T00:26:28.970Z,38.791832,-122.7884979,0.25,0.79,md,14,59,0.01191,0.03,nc,nc73679911,2022-01-18T00:28:07.049Z,"3km WNW of The Geysers, CA",earthquake,0.22,0.53,0.31,3,automatic,nc,nc
2022-01-18T00:24:39.090Z,35.032,-117.6818333,-0.78,1.67,ml,30,86,0.0981,0.16,ci,ci39915095,2022-01-18T18:15:22.565Z,"5km NW of Boron, CA",quarry blast,0.37,31.61,0.189,26,reviewed,ci,ci
2022-01-18T00:23:43.180Z,18.0165,-66.7711,14,1.99,md,8,85,0.1158,0.12,pr,pr2022018000,2022-01-18T00:36:39.678Z,"0 km WSW of Magas Arriba, Puerto Rico",earthquake,0.44,0.63,0.08,8,reviewed,pr,pr
2022-01-18T00:16:45.510Z,38.7924995,-122.7881699,-0.81,0.96,md,17,102,0.01237,0.04,nc,nc73679891,2022-01-18T00:18:21.130Z,"3km WNW of The Geysers, CA",earthquake,0.18,0.68,0.08,3,automatic,nc,nc
2022-01-18T00:16:34.750Z,38.7931671,-122.7876663,0.28,0.49,md,10,101,0.0001971,0.03,nc,nc73679886,2022-01-18T00:18:11.760Z,"3km WNW of The Geysers, CA",earthquake,0.3,0.5,0.35,2,automatic,nc,nc
2022-01-18T00:16:15.940Z,38.7946663,-122.7893295,0.04,1.4,md,13,93,0.00185,0.03,nc,nc73679881,2022-01-18T00:51:12.030Z,"3km NW of The Geysers, CA",earthquake,0.21,0.41,0.38,3,automatic,nc,nc
2022-01-18T00:15:45.820Z,64.7829,-149.7397,16.6,1.1,ml,,,,0.64,ak,ak022trrk5y,2022-01-18T00:20:10.786Z,"35 km NW of Four Mile Road, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-18T00:14:47.715Z,39.2245,-120.0854,8.7,0.4,ml,8,90.4,0.036,0.0775,nn,nn00831904,2022-01-19T02:38:17.204Z,"0 km SW of Carnelian Bay, California",earthquake,,1.4,0.04,3,reviewed,nn,nn
2022-01-18T00:12:23.000Z,43.6045,-110.3421667,5.27,1.36,ml,11,131,0.19,0.21,mb,mb80536234,2022-01-18T15:53:55.960Z,"22 km E of Kelly, Wyoming",earthquake,0.6,8.6,0.272,8,reviewed,mb,mb
2022-01-18T00:09:35.910Z,38.815834,-122.8191681,2.38,0.85,md,12,86,0.01037,0.02,nc,nc73679876,2022-01-18T00:11:11.895Z,"7km NW of The Geysers, CA",earthquake,0.32,0.86,,1,automatic,nc,nc
2022-01-18T00:03:37.330Z,38.8153343,-122.819664,2.15,2.3,md,42,42,0.009846,0.06,nc,nc73679871,2022-01-18T00:25:11.078Z,"7km NW of The Geysers, CA",earthquake,0.16,0.28,0.1,20,automatic,nc,nc
2022-01-18T00:03:22.140Z,38.8429985,-122.841835,1.57,0.37,md,7,149,0.00663,0.01,nc,nc73679866,2022-01-18T00:04:56.915Z,"10km NW of The Geysers, CA",earthquake,0.45,0.82,,1,automatic,nc,nc
2022-01-17T23:54:32.740Z,38.8308334,-122.8150024,2.39,0.75,md,14,67,0.008366,0.01,nc,nc73679856,2022-01-17T23:56:08.948Z,"8km NW of The Geysers, CA",earthquake,0.3,0.8,0.1,2,automatic,nc,nc
2022-01-17T23:39:02.090Z,35.8381667,-117.6325,10.83,0.74,ml,15,114,0.03618,0.08,ci,ci39915055,2022-01-18T23:32:16.902Z,"22km WNW of Searles Valley, CA",earthquake,0.17,0.29,0.02,3,reviewed,ci,ci
2022-01-17T23:38:43.440Z,35.6586667,-117.4478333,6.13,-0.03,ml,3,318,0.07295,0.1,ci,ci37379668,2022-01-18T23:35:02.921Z,"13km SSW of Searles Valley, CA",earthquake,5.21,5.65,0.095,1,reviewed,ci,ci
2022-01-17T23:38:23.310Z,38.8158333,-111.3578333,6.53,1.16,md,5,171,0.06267,0.06,uu,uu60477897,2022-01-18T17:37:44.720Z,"15 km SW of Emery, Utah",earthquake,1.67,3.33,0.079,4,reviewed,uu,uu
2022-01-17T23:37:54.228Z,58.3279,-155.0445,0.1,1.4,ml,,,,0.6,ak,ak022si1wzi,2022-01-19T22:31:00.930Z,"91 km NNW of Karluk, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-17T23:37:53.420Z,58.2948333333333,-154.991833333333,3.22,1.13,ml,8,166,,0.15,av,av91047373,2022-01-20T00:02:36.680Z,"86 km NNW of Karluk, Alaska",earthquake,0.58,0.64,0.228871785213344,8,reviewed,av,av
2022-01-17T23:31:46.310Z,46.8533333333333,-121.746333333333,0.02,0.56,ml,15,75,0.01993,0.07,uw,uw61802347,2022-01-18T19:35:01.850Z,"24 km ENE of Ashford, Washington",earthquake,0.2,0.64,0.10872407351084,8,reviewed,uw,uw
2022-01-17T23:31:08.641Z,59.5786,-152.9578,98.6,1.5,ml,,,,0.4,ak,ak022si0j6h,2022-01-17T23:43:46.459Z,"63 km WNW of Nanwalek, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T23:28:57.971Z,39.0468,35.9025,10,5.1,mwr,,36,0.199,1.06,us,us7000gcr9,2022-01-18T07:23:19.080Z,"6 km WSW of Sarıoğlan, Turkey",earthquake,3.9,1.8,0.062,25,reviewed,us,us
2022-01-17T23:09:45.180Z,33.7405,-116.8931667,5.36,0.34,ml,9,208,0.05909,0.06,ci,ci39915031,2022-01-18T18:46:22.770Z,"1km S of Valle Vista, CA",earthquake,0.33,0.47,0.074,3,reviewed,ci,ci
2022-01-17T23:07:02.930Z,35.6673333,-117.4723333,8.41,0.8,ml,17,112,0.08108,0.1,ci,ci39915023,2022-01-18T23:28:40.882Z,"13km SSW of Searles Valley, CA",earthquake,0.25,0.66,0.104,5,reviewed,ci,ci
2022-01-17T22:59:23.932Z,29.3194,94.2201,10,4.9,mb,,82,8.007,0.9,us,us7000gcr6,2022-01-17T23:12:36.040Z,"eastern Xizang-India border region",earthquake,7.8,1.9,0.101,31,reviewed,us,us
2022-01-17T22:58:20.750Z,34.4345,-119.2855,9.76,1.85,ml,40,49,0.03901,0.28,ci,ci39915015,2022-01-18T23:22:10.633Z,"4km WSW of Ojai, CA",earthquake,0.26,0.6,0.129,13,reviewed,ci,ci
2022-01-17T22:56:36.100Z,38.786335,-122.745163,1.93,0.66,md,15,83,0.007284,0.01,nc,nc73679851,2022-01-17T22:58:12.262Z,"1km NE of The Geysers, CA",earthquake,0.27,0.52,0.12,3,automatic,nc,nc
2022-01-17T22:55:12.020Z,51.7795,-175.7035,1.94,1.68,ml,9,309,,0.24,av,av91047368,2022-01-19T23:47:03.230Z,"65 km E of Adak, Alaska",earthquake,0.9,1.58,0.273712559683544,9,reviewed,av,av
2022-01-17T22:48:09.993Z,60.7709,-151.8061,80.9,1.8,ml,,,,0.54,ak,ak022shiqv0,2022-01-17T22:55:00.452Z,"29 km WNW of Nikiski, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T22:45:43.590Z,51.9088333333333,-176.552166666667,2.69,1.6,ml,8,144,,0.26,av,av91465741,2022-01-19T21:27:32.690Z,"6 km NE of Adak, Alaska",earthquake,0.7,0.96,0.281396050251528,8,reviewed,av,av
2022-01-17T22:31:30.120Z,46.1936666666667,-122.1905,3.45,0.41,ml,12,92,0.00612,0.09,uw,uw61802322,2022-01-18T19:41:03.290Z,"37 km NNE of Amboy, Washington",earthquake,0.28,0.41,0.112979253808522,4,reviewed,uw,uw
2022-01-17T22:30:43.630Z,38.8204994,-122.7881699,1.69,0.84,md,8,86,0.009298,0.01,nc,nc73679846,2022-01-17T22:32:21.095Z,"6km NNW of The Geysers, CA",earthquake,0.57,1.29,,1,automatic,nc,nc
2022-01-17T22:29:54.430Z,33.3366667,-117.141,-0.62,1.13,ml,25,90,0.05504,0.26,ci,ci39914975,2022-01-18T18:07:06.191Z,"7km WSW of Pala, CA",quarry blast,0.58,31.61,0.165,17,reviewed,ci,ci
2022-01-17T22:22:24.248Z,31.19772336,-103.3521609,7.494091797,2.2,ml,14,76,0.07172419487,0.3,tx,tx2022beyi,2022-01-19T02:55:05.839Z,"25 km SE of Lindsay, Texas",earthquake,1.667534166,1.813064474,0.1,11,reviewed,tx,tx
2022-01-17T22:15:51.070Z,38.8293343,-122.8021698,11.79,0.39,md,7,120,0.008561,0.05,nc,nc73679841,2022-01-17T22:17:27.319Z,"7km W of Cobb, CA",earthquake,1.43,2.48,,1,automatic,nc,nc
2022-01-17T22:13:55.490Z,19.1688327789307,-155.489669799805,35.1199989318848,2.18000007,md,45,145,,0.119999997,hv,hv72878977,2022-01-17T22:19:26.510Z,"3 km SSW of Pāhala, Hawaii",earthquake,0.55,0.810000002,1.37,23,automatic,hv,hv
2022-01-17T22:09:27.870Z,35.79916667,-96.65533333,7.56,2.17,ml,68,76,0.1349735136,0.23,ok,ok2022bexx,2022-01-18T22:46:59.495Z,"5 km N of Stroud, Oklahoma",earthquake,,0.5,0.18,13,reviewed,ok,ok
2022-01-17T22:01:07.780Z,41.8741667,-111.6465,6.1,1.77,md,6,134,0.2626,0.14,uu,uu60477882,2022-01-18T17:24:21.260Z,"14 km ESE of Richmond, Utah",earthquake,1.01,10.08,0.274,3,reviewed,uu,uu
2022-01-17T21:59:04.440Z,38.795166,-122.7603302,2.93,0.36,md,8,118,0.005472,0.03,nc,nc73679836,2022-01-17T22:00:41.401Z,"2km N of The Geysers, CA",earthquake,1,1.55,,1,automatic,nc,nc
2022-01-17T21:53:58.217Z,60.9228,-149.0639,20,0.5,ml,,,,0.55,ak,ak022sgygv3,2022-01-18T18:39:19.034Z,"5 km ESE of Girdwood, Alaska",earthquake,,2.7,,,reviewed,ak,ak
2022-01-17T21:41:52.970Z,19.2466,-67.3805,8,3.75,md,22,300,0.8243,0.26,pr,pr2022017003,2022-01-18T23:56:24.040Z,"88 km NNW of San Antonio, Puerto Rico",earthquake,5.28,7.59,0.11,22,reviewed,pr,pr
2022-01-17T21:40:53.470Z,35.8841667,-117.6883333,6.56,0.55,ml,14,79,0.07067,0.1,ci,ci39914943,2022-01-18T23:11:28.139Z,"20km ESE of Little Lake, CA",earthquake,0.17,0.48,0.088,4,reviewed,ci,ci
2022-01-17T21:39:00.486Z,61.0618,-148.3346,0,1.1,ml,,,,0.9,ak,ak022sgvd26,2022-01-17T21:43:12.090Z,"37 km NNE of Whittier, Alaska",earthquake,,1.3,,,automatic,ak,ak
2022-01-17T21:33:25.605Z,31.60555599,-103.9798133,7.879711914,2,ml,12,63,0.08172930709,0.1,tx,tx2022bewq,2022-01-23T05:36:54.657Z,"36 km NNW of Toyah, Texas",earthquake,0.9940538404,1.048435745,0.2,5,reviewed,tx,tx
2022-01-17T21:33:24.050Z,19.1513328552246,-155.480499267578,33.75,1.92999995,md,38,149,,0.109999999,hv,hv72878932,2022-01-17T21:36:31.600Z,"5 km S of Pāhala, Hawaii",earthquake,0.53,0.699999988,0.959999979,8,automatic,hv,hv
2022-01-17T21:26:45.960Z,38.7931671,-122.7631683,2.77,0.88,md,18,65,0.007922,0.03,nc,nc73679826,2022-01-17T21:28:22.450Z,"2km NNW of The Geysers, CA",earthquake,0.29,0.54,0.23,5,automatic,nc,nc
2022-01-17T21:22:02.960Z,60.4735,-140.4654,25.2,1.4,ml,,,,0.51,ak,ak022sgrq2w,2022-01-17T21:25:59.974Z,"111 km NNW of Yakutat, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-17T21:09:15.839Z,34.37066667,-96.85866667,0,1.91,ml,29,84,0.218657092,0.31,ok,ok2022bevx,2022-01-18T22:48:41.770Z,"4 km SW of Mill Creek, Oklahoma",quarry blast,,0.5,0.2,3,reviewed,ok,ok
2022-01-17T21:04:48.504Z,60.6636,-151.4871,54.2,1.1,ml,,,,0.4,ak,ak022sgnypf,2022-01-17T21:09:48.089Z,"10 km WNW of Salamatof, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-17T20:47:43.023Z,43.4597,-70.7943,5,2,ml,,219,0.571,0.22,us,us7000gd93,2022-01-19T22:57:46.040Z,"0 km S of Springvale, Maine",earthquake,2.6,1.9,0.128,11,reviewed,us,us
2022-01-17T20:47:21.789Z,62.854,-148.8798,61.6,1.6,ml,,,,0.54,ak,ak022sgbot9,2022-01-17T21:08:07.582Z,"60 km S of Cantwell, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-17T20:47:19.290Z,33.4841667,-116.4621667,12.26,0.97,ml,14,80,0.04959,0.23,ci,ci37379660,2022-01-18T23:08:46.739Z,"21km ESE of Anza, CA",earthquake,0.54,1.03,0.046,8,reviewed,ci,ci
2022-01-17T20:47:14.970Z,33.5,-116.4561667,13.87,0.63,ml,12,200,0.03453,0.15,ci,ci37379652,2022-01-18T23:02:49.696Z,"21km ESE of Anza, CA",earthquake,0.54,0.71,0.108,5,reviewed,ci,ci
2022-01-17T20:47:08.180Z,33.4898333,-116.4401667,12.46,1.18,ml,23,147,0.03559,0.17,ci,ci37379644,2022-01-18T22:57:48.673Z,"23km SSW of La Quinta, CA",earthquake,0.41,0.56,0.16,7,reviewed,ci,ci
2022-01-17T20:47:06.690Z,33.4956667,-116.4613333,9.78,0.77,ml,23,141,0.04064,0.13,ci,ci39914919,2022-01-18T22:45:23.598Z,"21km ESE of Anza, CA",earthquake,0.35,0.42,0.146,7,reviewed,ci,ci
2022-01-17T20:43:48.350Z,34.0445,-117.2455,16.57,1.63,ml,74,68,0.09799,0.19,ci,ci39914911,2022-01-18T22:37:29.080Z,"2km ESE of Loma Linda, CA",earthquake,0.17,0.38,0.194,22,reviewed,ci,ci
2022-01-17T20:42:36.000Z,40.3046667,-124.6483333,18.19,2.77,md,59,227,0.2344,0.19,nc,nc73679816,2022-01-18T09:01:11.023Z,"31km W of Petrolia, CA",earthquake,0.72,0.49,0.134,57,reviewed,nc,nc
2022-01-17T20:37:49.200Z,38.8396683,-122.8243332,1.97,0.86,md,9,99,0.008777,0.01,nc,nc73679811,2022-01-17T20:39:26.320Z,"9km WNW of Cobb, CA",earthquake,0.44,1.09,,1,automatic,nc,nc
2022-01-17T20:30:15.400Z,36.6625,-116.2766,6.4,0.2,ml,8,175.28,0.053,0.0641,nn,nn00831833,2022-01-17T20:33:12.801Z,"51 km ESE of Beatty, Nevada",earthquake,,2.1,0.18,5,automatic,nn,nn
2022-01-17T20:27:16.238Z,61.8804,-152.1713,118.4,1.5,ml,,,,0.43,ak,ak022sg7e2v,2022-01-17T20:32:42.046Z,"42 km WSW of Skwentna, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T20:23:10.180Z,33.5033333,-116.4918333,13.98,0.5,ml,23,61,0.05876,0.14,ci,ci39914903,2022-01-18T22:16:59.370Z,"18km ESE of Anza, CA",earthquake,0.28,0.48,0.227,9,reviewed,ci,ci
2022-01-17T20:19:43.583Z,59.6267,-152.4394,83.2,1.4,ml,,,,0.49,ak,ak022sg5qgl,2022-01-17T20:32:41.898Z,"38 km WSW of Anchor Point, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-17T20:02:33.970Z,46.021,-112.4473333,-2,1.38,ml,10,117,0.075,0.04,mb,mb80536319,2022-01-18T20:45:26.450Z,"7 km ESE of Walkerville, Montana",quarry blast,0.49,31.61,0.258,6,reviewed,mb,mb
2022-01-17T20:01:30.350Z,35.9461667,-117.6568333,4.31,0.43,ml,11,73,0.005515,0.1,ci,ci39914871,2022-01-18T22:09:35.369Z,"22km E of Little Lake, CA",earthquake,0.21,0.24,0.098,4,reviewed,ci,ci
2022-01-17T19:52:59.340Z,19.1889991760254,-155.484664916992,36.3400001525879,2.41000009,md,45,74,,0.109999999,hv,hv72878742,2022-01-17T19:56:20.450Z,"1 km SSW of Pāhala, Hawaii",earthquake,0.52,0.639999986,0.180000007,25,automatic,hv,hv
2022-01-17T19:32:47.139Z,-4.3685,129.5683,110.48,4.6,mb,,97,8.561,0.67,us,us7000gcpp,2022-01-17T20:37:25.040Z,"134 km SSE of Amahai, Indonesia",earthquake,12.6,9.3,0.096,32,reviewed,us,us
2022-01-17T19:30:44.660Z,36.7771667,-121.2805,11.69,1.12,md,18,106,0.07384,0.04,nc,nc73679806,2022-01-17T21:00:11.242Z,"4km ESE of Tres Pinos, CA",earthquake,0.22,0.44,0.266,17,reviewed,nc,nc
2022-01-17T19:28:48.970Z,38.8181648,-122.8079987,3.08,0.97,md,25,40,0.005468,0.02,nc,nc73679801,2022-01-17T19:42:07.207Z,"6km NW of The Geysers, CA",earthquake,0.22,0.48,0.09,4,automatic,nc,nc
2022-01-17T19:23:38.373Z,61.3424,-150.0591,18.9,2.1,ml,,,,0.95,ak,ak022sfl5ct,2022-01-17T19:35:31.515Z,"4 km WSW of Point MacKenzie, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-17T19:23:11.259Z,61.7156,-149.8932,25.8,2,ml,,,,0.97,ak,ak022sfl38c,2022-01-17T19:29:20.679Z,"8 km ESE of Willow, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-17T19:22:23.350Z,35.9731667,-117.3883333,3.12,1.29,ml,22,110,0.1183,0.11,ci,ci39914839,2022-01-18T22:03:00.332Z,"23km N of Searles Valley, CA",earthquake,0.22,0.61,0.209,10,reviewed,ci,ci
2022-01-17T19:20:09.930Z,39.4215,-110.3003333,-2.52,1.77,ml,10,199,0.01936,0.1,uu,uu60477867,2022-01-18T15:41:40.630Z,"16 km SSE of Sunnyside, Utah",earthquake,0.83,1.88,0.16,3,reviewed,uu,uu
2022-01-17T19:16:45.500Z,60.0528333333333,-153.081166666667,2.95,-0.78,ml,4,218,,0.16,av,av91465641,2022-01-19T20:58:16.680Z,"64 km ENE of Pedro Bay, Alaska",earthquake,0.9,1.34,0.193516297286523,4,reviewed,av,av
2022-01-17T19:09:33.953Z,61.8937,-149.5045,42.1,1.3,ml,,,,0.45,ak,ak022sfi4yb,2022-01-17T19:15:02.152Z,"21 km NW of Fishhook, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T19:07:23.640Z,35.12616667,-95.3,5.3,1.33,ml,32,165,0.03599293696,0.24,ok,ok2022berx,2022-01-18T22:20:07.318Z,"5 km W of Kinta, Oklahoma",earthquake,,0.5,0.29,7,reviewed,ok,ok
2022-01-17T19:00:39.530Z,38.8336678,-122.8168335,1.86,0.97,md,17,58,0.01154,0.02,nc,nc73679791,2022-01-17T19:02:18.947Z,"8km NW of The Geysers, CA",earthquake,0.23,0.49,0.21,3,automatic,nc,nc
2022-01-17T18:56:44.630Z,33.2721667,-116.1385,11.31,1.21,ml,45,37,0.1187,0.21,ci,ci39914799,2022-01-18T21:55:15.759Z,"14km N of Ocotillo Wells, CA",earthquake,0.21,0.5,0.139,17,reviewed,ci,ci
2022-01-17T18:52:46.119Z,35.13916667,-95.30266667,4.93,1.16,ml,33,161,0.03959223065,0.25,ok,ok2022berk,2022-01-18T22:11:42.022Z,"6 km WNW of Kinta, Oklahoma",earthquake,,0.6,0.43,5,reviewed,ok,ok
2022-01-17T18:41:47.547Z,62.3621,-149.0773,12.8,1.5,ml,,,,0.8,ak,ak022sf3lb6,2022-01-17T18:45:08.529Z,"45 km ENE of Susitna North, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-17T18:40:10.332Z,60.6253,-152.1493,86.1,1.5,ml,,,,0.51,ak,ak022sf3aqt,2022-01-17T18:43:28.195Z,"45 km W of Salamatof, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-17T18:19:57.720Z,38.7986679,-122.7753296,1.26,1.21,md,25,77,0.01126,0.04,nc,nc73679771,2022-01-17T19:59:11.629Z,"3km NW of The Geysers, CA",earthquake,0.2,0.32,0.03,6,automatic,nc,nc
2022-01-17T18:18:54.000Z,19.2083339691162,-155.515502929688,32.689998626709,2.07,ml,45,63,,0.140000001,hv,hv72878612,2022-01-17T18:24:25.180Z,"3 km W of Pāhala, Hawaii",earthquake,0.47,0.779999971,3.44,7,automatic,hv,hv
2022-01-17T18:13:35.400Z,39.4216667,-110.3091667,-1.82,1.68,ml,8,196,0.01258,0.13,uu,uu60477862,2022-01-18T17:12:28.310Z,"15 km SSE of Sunnyside, Utah",earthquake,1.12,0.93,0.091,2,reviewed,uu,uu
2022-01-17T18:07:31.804Z,37.9561,-118.0568,2.9,0.8,ml,8,192.67,0.148,0.143,nn,nn00831832,2022-01-17T18:11:29.912Z,"32 km N of Dyer, Nevada",earthquake,,1.4,0.24,4,automatic,nn,nn
2022-01-17T17:49:08.519Z,34.98833333,-97.70483333,10.88,1.31,ml,26,59,0.1133777514,0.29,ok,ok2022bepi,2022-01-18T21:55:16.466Z,"8 km SW of Dibble, Oklahoma",earthquake,,1.6,0.14,4,reviewed,ok,ok
2022-01-17T17:47:43.010Z,17.9556,-66.8718,9,2.41,md,16,190,0.0209,0.26,pr,pr2022017002,2022-01-17T18:25:24.983Z,"3 km SE of Maria Antonia, Puerto Rico",earthquake,0.49,0.57,0.29,12,reviewed,pr,pr
2022-01-17T17:42:46.710Z,19.216833114624,-155.401336669922,29.8999996185303,1.77999997,md,29,155,,0.150000006,hv,hv72878557,2022-01-17T17:45:49.240Z,"8 km E of Pāhala, Hawaii",earthquake,0.7,0.939999998,0.879999995,3,automatic,hv,hv
2022-01-17T17:39:59.632Z,-18.3875,-177.7634,561.91,4.4,mb,,128,4.031,0.68,us,us7000gcp6,2022-01-17T17:56:17.040Z,"Fiji region",earthquake,15.1,10.1,0.096,31,reviewed,us,us
2022-01-17T17:38:32.220Z,19.1030006408691,-155.685333251953,-0.310000002384186,1.7,ml,18,141,,0.219999999,hv,hv72878552,2022-01-17T17:44:02.490Z,"8 km WNW of Wai‘ōhinu, Hawaii",earthquake,0.63,0.430000007,3.86,3,automatic,hv,hv
2022-01-17T17:33:48.380Z,59.6205,-154.3495,179.8,1.6,ml,,,,1.34,ak,ak022segg1i,2022-01-17T17:59:13.089Z,"10 km NE of Pope-Vannoy Landing, Alaska",earthquake,,1.2,,,automatic,ak,ak
2022-01-17T17:32:18.650Z,35.6156667,-117.4233333,10.25,-0.16,ml,6,171,0.04301,0.09,ci,ci39914703,2022-01-18T18:44:17.755Z,"17km S of Searles Valley, CA",earthquake,0.68,0.42,0.145,2,reviewed,ci,ci
2022-01-17T17:23:47.170Z,33.7105,-117.0723333,11.75,0.97,ml,38,53,0.05907,0.18,ci,ci39914679,2022-01-18T17:59:43.946Z,"1km ENE of Winchester, CA",earthquake,0.24,0.47,0.209,22,reviewed,ci,ci
2022-01-17T17:22:20.558Z,38.1885,-117.7542,13,0.7,ml,9,214.21,0.117,0.1113,nn,nn00831831,2022-01-17T17:26:19.964Z,"38 km SE of Mina, Nevada",earthquake,,2.3,0.31,4,automatic,nn,nn
2022-01-17T17:19:48.810Z,38.8344994,-122.810997,2.13,0.97,md,22,52,0.01111,0.02,nc,nc73679766,2022-01-17T17:21:26.867Z,"8km W of Cobb, CA",earthquake,0.19,0.51,0.09,4,automatic,nc,nc
2022-01-17T17:11:54.370Z,38.757,-122.731,2.24,0.13,md,20,68,0.006639,0.04,nc,nc73679761,2022-01-20T21:53:17.085Z,"3km SE of The Geysers, CA",earthquake,0.21,0.31,0.101,4,reviewed,nc,nc
2022-01-17T17:06:46.820Z,38.7551667,-122.732,1.47,0.12,md,10,125,0.008505,0.04,nc,nc71127059,2022-01-19T09:14:50.473Z,"3km SE of The Geysers, CA",earthquake,0.41,0.49,0.188,3,reviewed,nc,nc
2022-01-17T17:06:29.990Z,39.632,-122.5785,10.22,1.8,md,16,97,0.1406,0.26,nc,nc73679756,2022-01-19T09:14:11.144Z,"7km NW of Stony Gorge Reservoir, CA",earthquake,0.61,2.3,0.173,19,reviewed,nc,nc
2022-01-17T17:02:33.160Z,51.6541666666667,-179.198333333333,9.35,2.65,ml,18,143,,0.23,av,av91465561,2022-01-19T20:16:08.510Z,"178 km W of Adak, Alaska",earthquake,0.76,0.67,0.234056950711871,23,reviewed,av,av
2022-01-17T16:58:19.850Z,38.8445,-122.816,1.83,1.19,md,32,48,0.01166,0.03,nc,nc73679751,2022-01-22T09:36:10.636Z,"8km WNW of Cobb, CA",earthquake,0.16,0.28,0.06,6,reviewed,nc,nc
2022-01-17T16:57:50.520Z,19.1681671142578,-155.477340698242,33.6199989318848,1.72000003,md,35,157,,0.0900000036,hv,hv72878512,2022-01-17T17:01:09.930Z,"3 km S of Pāhala, Hawaii",earthquake,0.64,0.75,1.78999996,4,automatic,hv,hv
2022-01-17T16:49:04.780Z,36.21683333,-95.84566667,0,1.58,ml,43,201,0.3095392578,0.37,ok,ok2022beni,2022-01-18T20:31:32.023Z,"5 km S of Owasso, Oklahoma",quarry blast,,0.5,0.34,8,reviewed,ok,ok
2022-01-17T16:43:38.630Z,19.2714996337891,-155.261840820312,24.8899993896484,1.84,ml,43,150,,0.129999995,hv,hv72878492,2022-01-17T16:49:09.440Z,"19 km S of Volcano, Hawaii",earthquake,0.72,0.50999999,0.33,4,automatic,hv,hv
2022-01-17T16:40:09.590Z,38.7905006,-122.7606659,1.73,0.76,md,15,67,0.01014,0.03,nc,nc73679746,2022-01-17T16:41:47.953Z,"2km NNW of The Geysers, CA",earthquake,0.26,0.52,0.42,3,automatic,nc,nc
2022-01-17T16:31:09.478Z,36.6353,-116.2535,2.1,0.4,ml,9,211.91,0.069,0.1562,nn,nn00831830,2022-01-17T16:34:21.351Z,"52 km W of Indian Springs, Nevada",earthquake,,1.1,0.25,6,automatic,nn,nn
2022-01-17T16:30:01.014Z,64.7024,-148.6074,14.8,1.3,ml,,,,0.37,ak,ak022sdu9n2,2022-01-17T16:40:34.096Z,"26 km ENE of Four Mile Road, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-17T16:24:18.190Z,38.487,-122.5326667,9.29,1.32,md,27,86,0.07346,0.08,nc,nc73679741,2022-01-17T22:17:12.136Z,"6km WSW of St. Helena, CA",earthquake,0.21,0.33,0.135,18,reviewed,nc,nc
2022-01-17T16:03:03.651Z,62.9995,-150.5132,92.1,1.4,ml,,,,0.79,ak,ak022sdohi2,2022-01-17T16:06:30.076Z,"57 km NNE of Petersville, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-17T15:56:20.910Z,33.8178333,-118.2535,11.58,2.32,ml,70,64,0.05002,0.29,ci,ci39914591,2022-01-19T22:11:48.978Z,"3km ESE of Carson, CA",earthquake,0.27,0.4,0.185,64,reviewed,ci,ci
2022-01-17T15:56:15.370Z,38.8353348,-122.8176651,1.9,0.85,md,5,150,0.01332,0,nc,nc73679736,2022-01-17T15:57:50.763Z,"8km W of Cobb, CA",earthquake,0.74,1.43,,1,automatic,nc,nc
2022-01-17T15:52:01.290Z,38.8251648,-122.8526688,1.79,0.86,md,12,110,0.004054,0.01,nc,nc73679731,2022-01-17T15:53:35.980Z,"10km WNW of The Geysers, CA",earthquake,0.35,0.78,,1,automatic,nc,nc
2022-01-17T15:44:14.587Z,-26.7945,-176.4566,42.58,5,mb,,116,2.777,0.62,us,us7000gcmk,2022-01-17T16:53:39.040Z,"south of the Fiji Islands",earthquake,11.7,6.1,0.06,88,reviewed,us,us
2022-01-17T15:42:29.370Z,38.8426666,-122.8164978,0.83,0.86,md,9,91,0.01312,0.01,nc,nc73679726,2022-01-17T15:44:05.238Z,"8km WNW of Cobb, CA",earthquake,0.3,1.06,,1,automatic,nc,nc
2022-01-17T15:41:26.610Z,32.6846667,-115.3783333,15.26,1.93,ml,28,61,0.07703,0.18,ci,ci39914567,2022-01-18T23:44:06.757Z,"9km ENE of Mexicali, B.C., MX",earthquake,0.3,0.47,0.123,15,reviewed,ci,ci
2022-01-17T15:32:33.060Z,61.0237,-153.4233,25.3,1.1,ml,,,,0.69,ak,ak022sd9bin,2022-01-17T15:36:36.464Z,"103 km NNE of Port Alsworth, Alaska",earthquake,,1.3,,,automatic,ak,ak
2022-01-17T15:25:17.703Z,59.9397,-140.506,5.2,1.6,ml,,,,0.71,ak,ak022sd7sqi,2022-01-17T15:30:25.641Z,"61 km NW of Yakutat, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-17T15:08:51.980Z,19.1776676177979,-155.476333618164,31.4899997711182,2.13000011,md,49,77,,0.119999997,hv,hv72878427,2022-01-17T15:14:23.600Z,"2 km S of Pāhala, Hawaii",earthquake,0.57,0.75999999,1.72000003,18,automatic,hv,hv
2022-01-17T15:08:27.820Z,38.8283333,-122.766,0.99,0.09,md,9,116,0.003728,0.02,nc,nc73679721,2022-01-22T07:45:17.710Z,"4km W of Cobb, CA",earthquake,0.55,0.75,0.202,3,reviewed,nc,nc
2022-01-17T15:04:45.467Z,44.789,95.1305,10,5.5,mb,,29,8.371,0.77,us,us7000gcmh,2022-01-18T15:08:23.984Z,"196 km SSW of Altai, Mongolia",earthquake,5.8,1.8,0.028,442,reviewed,us,us
2022-01-17T14:47:25.610Z,36.1676667,-118.0228333,1.63,1.51,ml,17,64,0.1449,0.13,ci,ci39914543,2022-01-18T14:39:57.525Z,"13km S of Olancha, CA",earthquake,0.24,0.53,0.157,20,reviewed,ci,ci
2022-01-17T14:43:38.900Z,38.8450012,-122.817337,1.43,0.86,md,17,63,0.01073,0.01,nc,nc73679706,2022-01-17T14:45:16.087Z,"9km WNW of Cobb, CA",earthquake,0.22,0.42,,1,automatic,nc,nc
2022-01-17T14:38:34.588Z,61.6893,-150.6178,55.9,1.8,ml,,,,0.71,ak,ak022scp6pn,2022-01-17T14:42:59.996Z,"17 km NNW of Susitna, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T14:36:59.754Z,31.68715438,-104.3995917,6.080151367,2.4,ml,23,68,0.08822964674,0.2,tx,tx2022beja,2022-01-18T23:22:41.516Z,"54 km S of Whites City, New Mexico",earthquake,0.8868770081,1.400669602,0.1,12,reviewed,tx,tx
2022-01-17T14:31:50.030Z,38.8271675,-122.8528366,2.01,0.98,md,6,101,0.01449,0.01,nc,nc73679701,2022-01-17T14:33:25.184Z,"10km WNW of The Geysers, CA",earthquake,0.41,1.57,0.61,2,automatic,nc,nc
2022-01-17T14:26:08.030Z,59.966,-152.9975,4.06,-0.86,ml,4,268,,0.04,av,av91465521,2022-01-19T18:50:41.600Z,"65 km ENE of Pedro Bay, Alaska",earthquake,0.66,0.92,0.178639577553129,4,reviewed,av,av
2022-01-17T14:19:26.853Z,60.4124,-151.0676,34.7,1.7,ml,,,,0.8,ak,ak022scl3jh,2022-01-17T14:41:19.457Z,"8 km S of Soldotna, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-17T14:16:56.960Z,38.8056679,-122.7786636,1.82,0.72,md,13,68,0.007743,0.02,nc,nc73679696,2022-01-17T14:18:31.590Z,"4km NNW of The Geysers, CA",earthquake,0.37,0.59,0.14,2,automatic,nc,nc
2022-01-17T14:14:27.136Z,59.8964,-153.1919,117.8,1.7,ml,,,,0.37,ak,ak022sck0yu,2022-01-17T14:41:19.307Z,"52 km ENE of Pedro Bay, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T14:14:17.720Z,35.8541667,-117.6908333,8.16,0.48,ml,14,75,0.07544,0.09,ci,ci39914527,2022-01-18T23:46:06.974Z,"22km ESE of Little Lake, CA",earthquake,0.17,0.47,0.083,6,reviewed,ci,ci
2022-01-17T14:13:30.308Z,57.9948,-137.6046,6.2,2.4,ml,,,,0.53,ak,ak022scjtez,2022-01-17T16:34:51.040Z,"77 km WSW of Elfin Cove, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-17T14:12:49.010Z,38.8404999,-122.8411636,1.92,1.19,md,20,87,0.004826,0.03,nc,nc73679691,2022-01-17T14:45:12.067Z,"10km NW of The Geysers, CA",earthquake,0.24,0.41,0.02,4,automatic,nc,nc
2022-01-17T14:05:19.490Z,19.1863327026367,-155.474670410156,34.2999992370605,1.78999996,md,34,198,,0.100000001,hv,hv72878337,2022-01-17T14:08:39.120Z,"1 km SSE of Pāhala, Hawaii",earthquake,0.72,0.600000024,0.600000024,3,automatic,hv,hv
2022-01-17T13:57:47.690Z,46.2003333333333,-122.185833333333,3.5,0.09,ml,12,126,0.0002672,0.11,uw,uw61802212,2022-01-17T17:25:07.520Z,"38 km NNE of Amboy, Washington",earthquake,0.47,0.56,0.0788793676451317,3,reviewed,uw,uw
2022-01-17T13:51:58.539Z,36.51483333,-99.26016667,6.86,1.53,ml,24,163,0.1808645082,0.12,ok,ok2022behm,2022-01-18T20:18:36.755Z,"9 km NNW of Mooreland, Oklahoma",earthquake,,0.4,0.18,6,reviewed,ok,ok
2022-01-17T13:50:40.680Z,38.8243332,-122.7854996,0.7,0.35,md,7,98,0.01168,0.02,nc,nc73679686,2022-01-17T13:52:16.586Z,"5km W of Cobb, CA",earthquake,0.41,1.6,,1,automatic,nc,nc
2022-01-17T13:45:27.310Z,40.3888333,-124.2601667,24.33,1.61,md,20,113,0.06929,0.1,nc,nc73679681,2022-01-18T06:16:11.040Z,"7km NNE of Petrolia, CA",earthquake,0.54,0.44,0.21,10,reviewed,nc,nc
2022-01-17T13:45:02.214Z,63.2169,-150.5238,112.7,1.8,ml,,,,0.4,ak,ak022sc56nx,2022-01-17T13:53:22.854Z,"70 km ESE of Denali National Park, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-17T13:44:35.240Z,38.4843333,-112.8426667,2.42,0.46,md,8,106,0.02558,0.05,uu,uu60477852,2022-01-18T17:08:50.250Z,"17 km ENE of Milford, Utah",earthquake,0.34,0.91,0.345,4,reviewed,uu,uu
2022-01-17T13:42:01.610Z,35.5933333,-117.3915,7.97,1.83,ml,37,96,0.05803,0.13,ci,ci39914495,2022-01-18T23:56:14.580Z,"19km S of Trona, CA",earthquake,0.15,0.36,0.164,23,reviewed,ci,ci
2022-01-17T13:40:26.280Z,19.2148342132568,-155.427993774414,34.0400009155273,2.25,ml,48,134,,0.109999999,hv,hv72878312,2022-01-17T13:45:57.150Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.48,0.579999983,2.74,6,automatic,hv,hv
2022-01-17T13:36:58.324Z,61.2961,-151.1038,61.4,1.4,ml,,,,0.45,ak,ak022sc3dja,2022-01-18T18:22:56.869Z,"17 km N of Beluga, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-17T13:34:20.000Z,35.7988333,-117.6176667,7.84,0.78,ml,18,98,0.02352,0.15,ci,ci39914487,2022-01-18T18:41:54.732Z,"20km W of Searles Valley, CA",earthquake,0.23,0.46,0.1,6,reviewed,ci,ci
2022-01-17T13:27:45.154Z,54.3893,-162.5676,35,3.6,ml,,180,0.68,0.79,us,us7000gcm1,2022-01-17T16:08:48.040Z,"75 km SE of False Pass, Alaska",earthquake,6.7,2,0.077,22,reviewed,us,us
2022-01-17T13:26:01.540Z,38.8321648,-122.8073349,2.13,0.36,md,8,93,0.009015,0.03,nc,nc73679676,2022-01-17T13:27:35.266Z,"7km W of Cobb, CA",earthquake,0.48,1.36,,1,automatic,nc,nc
2022-01-17T13:24:11.960Z,19.1948333333333,-155.522166666667,33.31,1.45,md,20,139,,0.1,hv,hv72878297,2022-01-18T21:04:29.180Z,"4 km W of Pāhala, Hawaii",earthquake,0.57,0.76,0.053738856044344,10,reviewed,hv,hv
2022-01-17T13:13:39.890Z,38.814167,-122.8286667,1.71,0.85,md,7,91,0.005306,0.02,nc,nc73679671,2022-01-17T13:15:16.824Z,"8km WNW of The Geysers, CA",earthquake,0.45,1,,1,automatic,nc,nc
2022-01-17T13:03:41.790Z,38.8358345,-122.8040009,1.84,0.85,md,9,110,0.01097,0.02,nc,nc73679666,2022-01-17T13:05:15.966Z,"7km WNW of Cobb, CA",earthquake,0.43,1.2,,1,automatic,nc,nc
2022-01-17T13:00:15.716Z,-20.4407,-178.2605,551.36,4.3,mb,,164,4.398,0.61,us,us7000gcm0,2022-01-17T15:56:44.040Z,"Fiji region",earthquake,13.1,7.8,0.089,36,reviewed,us,us
2022-01-17T12:47:16.601Z,35.3219,25.214,28.19,4.3,mb,,96,0.267,0.45,us,us7000gclz,2022-01-17T13:50:55.040Z,"4 km W of Kokkíni Cháni, Greece",earthquake,8.8,3.7,0.138,16,reviewed,us,us
2022-01-17T12:33:15.980Z,38.8243332,-122.765831,2.21,0.45,md,10,122,0.006909,0.02,nc,nc73679661,2022-01-17T12:34:51.808Z,"4km W of Cobb, CA",earthquake,0.38,0.7,0.4,2,automatic,nc,nc
2022-01-17T12:29:26.460Z,38.8250008,-122.8551636,2.2,0.37,md,13,65,0.01584,0.02,nc,nc73679656,2022-01-17T12:31:01.766Z,"10km WNW of The Geysers, CA",earthquake,0.27,0.86,,1,automatic,nc,nc
2022-01-17T12:28:13.170Z,60.5308333333333,-152.975,11.88,-0.58,ml,6,257,,0.08,av,av91465431,2022-01-19T18:35:35.990Z,"82 km ENE of Port Alsworth, Alaska",earthquake,0.63,0.54,0.151600511956366,6,reviewed,av,av
2022-01-17T12:24:57.600Z,38.675,-122.4028333,8.48,1.68,md,50,101,0.04499,0.11,nc,nc73679651,2022-01-22T23:07:10.879Z,"12km NNE of Angwin, CA",earthquake,0.23,0.28,0.223,29,reviewed,nc,nc
2022-01-17T12:12:34.590Z,37.5406667,-118.8428333,9.24,0.3,md,15,227,0.05047,0.04,nc,nc73679646,2022-01-17T16:49:48.456Z,"14km W of Toms Place, CA",earthquake,0.79,1.27,0.152,13,reviewed,nc,nc
2022-01-17T12:12:12.520Z,35.8935,-117.719,8.52,1.25,ml,28,38,0.07778,0.12,ci,ci39914471,2022-01-19T16:02:33.505Z,"18km ESE of Little Lake, CA",earthquake,0.13,0.37,0.243,12,reviewed,ci,ci
2022-01-17T12:06:27.214Z,61.8252,-149.8531,76.2,1.4,ml,,,,0.79,ak,ak022sbbg1t,2022-01-17T12:29:18.416Z,"13 km NE of Willow, Alaska",earthquake,,1.6,,,automatic,ak,ak
2022-01-17T11:58:36.640Z,19.2024993896484,-155.399169921875,31.5900001525879,1.85000002,md,42,165,,0.119999997,hv,hv72878212,2022-01-17T12:01:47.060Z,"8 km E of Pāhala, Hawaii",earthquake,0.7,0.819999993,1.62,6,automatic,hv,hv
2022-01-17T11:43:06.290Z,36.51866667,-99.262,6.64,1.75,ml,41,69,0.1817643316,0.15,ok,ok2022bedg,2022-01-18T19:27:00.645Z,"Oklahoma",earthquake,,0.4,0.17,5,reviewed,ok,ok
2022-01-17T11:40:08.179Z,34.946,63.5797,18.82,5.3,mww,,43,6.071,0.77,us,us7000gclu,2022-01-19T12:49:31.324Z,"41 km E of Qala i Naw, Afghanistan",earthquake,7.3,4,0.083,14,reviewed,us,us
2022-01-17T11:38:43.800Z,38.8363342,-122.8119965,1.98,1.13,md,23,45,0.01301,0.03,nc,nc73679641,2022-01-17T12:11:13.438Z,"8km WNW of Cobb, CA",earthquake,0.19,0.46,0.28,4,automatic,nc,nc
2022-01-17T11:19:59.830Z,33.5958333,-116.8071667,7,0.63,ml,25,47,0.04807,0.11,ci,ci39914463,2022-01-18T14:40:38.510Z,"13km WNW of Anza, CA",earthquake,0.19,0.39,0.187,15,reviewed,ci,ci
2022-01-17T11:18:42.040Z,36.0588333,-117.8518333,2.48,0.77,ml,17,72,0.05868,0.07,ci,ci39914455,2022-01-19T16:02:14.230Z,"9km E of Coso Junction, CA",earthquake,0.11,0.12,0.102,9,reviewed,ci,ci
2022-01-17T11:16:15.560Z,36.26033333,-97.57783333,6.24,0.89,ml,53,46,0.129574573,0.18,ok,ok2022becj,2022-01-18T18:57:09.576Z,"5 km S of Covington, Oklahoma",earthquake,,0.4,0.22,8,reviewed,ok,ok
2022-01-17T11:09:33.670Z,38.8310013,-122.8148346,2.23,0.85,md,9,83,0.008457,0.01,nc,nc73679636,2022-01-17T11:11:10.590Z,"8km NW of The Geysers, CA",earthquake,0.42,1.14,,1,automatic,nc,nc
2022-01-17T10:59:39.770Z,37.5948333,-118.795,4.96,-0.18,md,7,271,0.02752,0.01,nc,nc73679631,2022-01-17T16:40:17.092Z,"11km WNW of Toms Place, CA",earthquake,1.35,0.77,0.1,7,reviewed,nc,nc
2022-01-17T10:55:38.370Z,41.973,-112.4533333,0.5,0.85,md,10,113,0.1054,0.12,uu,uu60477847,2022-01-18T16:44:02.680Z,"17 km W of Portage, Utah",earthquake,0.38,8.3,0.213,8,reviewed,uu,uu
2022-01-17T10:53:53.020Z,32.1586667,-116.5073333,17.08,1.49,ml,17,275,0.2031,0.18,ci,ci39914447,2022-01-18T16:44:52.143Z,"33km NNE of El Sauzal, B.C., MX",earthquake,0.68,0.96,0.146,8,reviewed,ci,ci
2022-01-17T10:48:30.390Z,36.088,-117.8635,3.5,0.84,ml,11,147,0.03034,0.08,ci,ci39914439,2022-01-18T14:41:19.514Z,"9km ENE of Coso Junction, CA",earthquake,0.24,0.34,0.23,8,reviewed,ci,ci
2022-01-17T10:46:27.177Z,43.4647,-70.8201,5,2,ml,,144,0.554,0.5,us,us7000gd8d,2022-01-20T16:20:14.453Z,"2 km W of Springvale, Maine",earthquake,1.4,1.9,0.088,17,reviewed,us,us
2022-01-17T10:38:51.999Z,62.8823,-150.5797,107.7,1.7,ml,,,,0.75,ak,ak022sabhnz,2022-01-17T10:42:20.889Z,"44 km NNE of Petersville, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T10:37:35.530Z,33.9261667,-116.9278333,5.07,1.2,ml,62,67,0.04412,0.14,ci,ci39914431,2022-01-19T15:57:45.650Z,"5km E of Beaumont, CA",earthquake,0.11,0.45,0.185,43,reviewed,ci,ci
2022-01-17T10:37:04.318Z,38.1901,-117.8587,0,1.5,ml,15,146.48,0.094,0.3414,nn,nn00831825,2022-01-22T01:03:07.902Z,"31 km SE of Mina, Nevada",earthquake,,0,0.62,5,reviewed,nn,nn
2022-01-17T10:30:48.503Z,59.9629,-151.0239,56.2,1.2,ml,,,,0.29,ak,ak022sa9ro2,2022-01-17T10:34:09.871Z,"12 km NNW of Fox River, Alaska",earthquake,,1.6,,,automatic,ak,ak
2022-01-17T10:29:22.250Z,33.8213333,-117.8581667,6.04,0.73,ml,19,189,0.03513,0.18,ci,ci39914423,2022-01-19T15:44:01.582Z,"3km NW of Orange, CA",earthquake,0.43,0.61,0.107,6,reviewed,ci,ci
2022-01-17T10:25:53.500Z,19.1688327789307,-155.471328735352,34.9199981689453,1.80999994,md,44,83,,0.100000001,hv,hv72878127,2022-01-17T10:29:02.160Z,"3 km SSE of Pāhala, Hawaii",earthquake,0.61,0.670000017,1.71000004,10,automatic,hv,hv
2022-01-17T10:13:31.800Z,38.8120003,-122.8276672,2.04,0.38,md,14,59,0.01187,0.02,nc,nc73679626,2022-01-17T10:15:06.703Z,"7km WNW of The Geysers, CA",earthquake,0.25,0.69,0.32,2,automatic,nc,nc
2022-01-17T10:10:11.030Z,19.2180004119873,-155.425827026367,33.7000007629395,2.1,ml,47,133,,0.119999997,hv,hv72878117,2022-01-17T10:15:42.880Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.51,0.589999974,4.45,5,automatic,hv,hv
2022-01-17T10:08:39.320Z,37.573,-119.0098333,2.22,0.4,md,15,132,0.03959,0.03,nc,nc73679621,2022-01-17T16:37:17.479Z,"8km SSW of Mammoth Lakes, CA",earthquake,0.62,0.43,0.179,14,reviewed,nc,nc
2022-01-17T10:04:06.970Z,38.8245,-122.7975,3.15,0.26,md,10,63,0.009884,0.01,nc,nc73679616,2022-01-22T07:34:16.642Z,"6km NW of The Geysers, CA",earthquake,0.47,0.94,0.296,2,reviewed,nc,nc
2022-01-17T10:02:20.810Z,45.0673333333333,-122.328666666667,2.9,1.15,ml,10,106,0.129,0.25,uw,uw61802207,2022-01-17T17:17:55.900Z,"21 km ESE of Molalla, Oregon",earthquake,0.58,2.45,0.148919138755719,4,reviewed,uw,uw
2022-01-17T09:58:58.839Z,64.6986,-147.5278,10.9,0.7,ml,,,,0.43,ak,ak022s9ucwr,2022-01-17T10:02:26.407Z,"10 km SW of North Pole, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T09:52:55.920Z,33.3231667,-116.307,11.12,1.15,ml,39,65,0.03916,0.22,ci,ci39914415,2022-01-18T14:41:54.519Z,"10km NE of Borrego Springs, CA",earthquake,0.3,0.48,0.164,26,reviewed,ci,ci
2022-01-17T09:45:49.970Z,18.2923,-65.3035,23,3.51,md,18,179,0.0259,0.05,pr,pr2022017001,2022-01-18T08:25:56.040Z,"1 km SSW of Culebra, Puerto Rico",earthquake,1.42,0.84,0.16,10,reviewed,pr,pr
2022-01-17T09:35:57.055Z,34.8854,63.6704,10,4.9,mb,,92,6.027,0.98,us,us7000gcle,2022-01-17T10:09:16.040Z,"50 km ESE of Qala i Naw, Afghanistan",earthquake,7,1.8,0.055,104,reviewed,us,us
2022-01-17T09:28:14.779Z,59.5913,-152.8579,90.8,1.5,ml,,,,0.58,ak,ak022s9nu11,2022-01-17T10:02:26.259Z,"59 km WNW of Nanwalek, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T09:21:54.910Z,39.3398333,-123.247,7.12,1.27,md,17,57,0.05198,0.07,nc,nc73679601,2022-01-18T11:49:11.400Z,"9km NNW of Redwood Valley, CA",earthquake,0.19,0.46,0.158,13,reviewed,nc,nc
2022-01-17T09:19:07.500Z,19.3625,-155.059666666667,6.7,2.22,ml,49,166,,0.14,hv,hv72878072,2022-01-18T20:58:03.500Z,"13 km SE of Fern Forest, Hawaii",earthquake,0.45,0.32,0.174247629091792,25,reviewed,hv,hv
2022-01-17T09:18:11.900Z,38.7869987,-122.7651672,1.73,0.83,md,17,73,0.01426,0.03,nc,nc73679591,2022-01-17T09:19:45.775Z,"1km NW of The Geysers, CA",earthquake,0.24,0.49,0.3,3,automatic,nc,nc
2022-01-17T09:17:27.070Z,37.5696667,-118.8506667,2.81,-0.04,md,8,270,0.02658,0.04,nc,nc73679596,2022-01-17T16:30:49.826Z,"14km ESE of Mammoth Lakes, CA",earthquake,2.2,1.97,0.165,8,reviewed,nc,nc
2022-01-17T09:15:30.950Z,39.1285,-123.1061667,10.51,1.28,md,16,93,0.1374,0.11,nc,nc73679586,2022-01-17T19:57:13.623Z,"5km E of Talmage, CA",earthquake,0.24,1.17,0.139,14,reviewed,nc,nc
2022-01-17T09:12:20.920Z,38.8261681,-122.8550034,2.62,0.37,md,7,143,0.002006,0.01,nc,nc73679581,2022-01-17T09:13:55.904Z,"10km WNW of The Geysers, CA",earthquake,0.49,0.69,0.01,2,automatic,nc,nc
2022-01-17T09:11:32.173Z,38.1758,-117.9401,4.3,0.5,ml,10,151.74,0.04,0.1127,nn,nn00831824,2022-01-17T09:15:57.562Z,"Nevada",earthquake,,0.9,0.11,3,automatic,nn,nn
2022-01-17T09:09:52.530Z,62.9188,-150.9339,95.8,1.6,ml,,,,0.39,ak,ak022s9juck,2022-01-17T09:21:01.649Z,"47 km N of Petersville, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-17T09:07:50.454Z,-17.9575,-73.4001,10,4.5,mb,,143,2.936,0.69,us,us7000gcl9,2022-01-17T09:50:29.040Z,"164 km SSW of Camaná, Peru",earthquake,9.4,1.9,0.07,60,reviewed,us,us
2022-01-17T09:02:38.116Z,47.4138,-70.1346,19.22,1.8,ml,,166,0.187,0.22,us,us7000gdct,2022-01-19T23:16:35.040Z,"9 km NW of La Pocatière, Canada",earthquake,5.7,8.3,0.148,6,reviewed,us,us
2022-01-17T09:02:16.040Z,33.1546667,-116.0135,7.62,1.3,ml,51,50,0.1272,0.18,ci,ci39914399,2022-01-19T15:25:33.480Z,"11km E of Ocotillo Wells, CA",earthquake,0.18,0.63,0.167,34,reviewed,ci,ci
2022-01-17T08:58:41.610Z,33.4843333,-116.4315,14.14,0.41,ml,20,78,0.03926,0.14,ci,ci39914391,2022-01-18T22:01:39.380Z,"23km SSW of La Quinta, CA",earthquake,0.25,0.62,0.142,7,reviewed,ci,ci
2022-01-17T08:42:49.174Z,-31.7628,-68.8464,10,4.2,mb,,90,0.256,0.36,us,us7000gcl7,2022-01-17T09:36:36.040Z,"25 km SSW of Villa Basilio Nievas, Argentina",earthquake,4.9,1.9,0.176,9,reviewed,us,us
2022-01-17T08:38:53.660Z,19.1798324584961,-155.47966003418,37.0699996948242,2.07999992,md,45,74,,0.100000001,hv,hv72878057,2022-01-17T08:42:14.840Z,"2 km S of Pāhala, Hawaii",earthquake,0.48,0.600000024,0.469999999,13,automatic,hv,hv
2022-01-17T08:35:59.865Z,61.3524,-151.0528,58.6,1.3,ml,,,,0.74,ak,ak022s93zwy,2022-01-17T08:40:26.899Z,"23 km N of Beluga, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T08:29:05.619Z,36.63,-116.253,0,0.3,ml,8,227.54,0.071,0.1538,nn,nn00831823,2022-01-17T08:32:17.746Z,"52 km W of Indian Springs, Nevada",earthquake,,9.9,0.07,3,automatic,nn,nn
2022-01-17T08:22:33.409Z,61.661,-142.0952,0,2,ml,,,,0.72,ak,ak022s915k9,2022-01-17T08:40:26.754Z,"50 km ENE of McCarthy, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-17T08:17:15.960Z,36.0705,-117.8648333,2.5,0.92,ml,19,71,0.04767,0.08,ci,ci39914383,2022-01-18T21:55:21.339Z,"8km ENE of Coso Junction, CA",earthquake,0.13,0.14,0.062,6,reviewed,ci,ci
2022-01-17T08:09:35.690Z,36.1336667,-118.0641667,3.63,1.47,ml,29,52,0.09043,0.15,ci,ci39914375,2022-01-18T21:51:32.311Z,"14km NW of Coso Junction, CA",earthquake,0.19,0.65,0.113,11,reviewed,ci,ci
2022-01-17T07:58:49.600Z,39.2304,-120.0877,9,0.7,ml,9,117.45,0.037,0.105,nn,nn00831822,2022-01-17T08:02:08.034Z,"0 km NW of Carnelian Bay, California",earthquake,,0.8,0.17,5,automatic,nn,nn
2022-01-17T07:57:50.438Z,36.6569,-116.2822,9.4,0.5,ml,8,182.34,0.047,0.063,nn,nn00831821,2022-01-17T08:00:57.624Z,"50 km ESE of Beatty, Nevada",earthquake,,1.9,0.12,3,automatic,nn,nn
2022-01-17T07:56:58.840Z,35.7735,-117.5815,7.35,0.86,ml,14,149,0.04411,0.14,ci,ci39914367,2022-01-18T14:42:34.521Z,"16km W of Searles Valley, CA",earthquake,0.38,0.74,0.114,10,reviewed,ci,ci
2022-01-17T07:55:04.641Z,61.7204,-151.779,94.2,1.8,ml,,,,0.67,ak,ak022s8mqdw,2022-01-17T08:08:02.407Z,"36 km SSW of Skwentna, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T07:53:57.420Z,35.9086667,-117.6905,4.33,1.18,ml,28,35,0.05092,0.11,ci,ci39914359,2022-01-18T21:45:34.724Z,"20km E of Little Lake, CA",earthquake,0.12,0.31,0.157,15,reviewed,ci,ci
2022-01-17T07:35:17.830Z,19.2183333333333,-155.409666666667,32.87,1.87,md,47,149,,0.11,hv,hv72878002,2022-01-18T20:35:08.600Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.41,0.55,0.204327221311475,22,reviewed,hv,hv
2022-01-17T07:33:09.070Z,36.7405014,-121.3243332,4.9,1.61,md,9,166,0.03748,0.32,nc,nc73679571,2022-01-17T08:07:11.958Z,"6km S of Tres Pinos, CA",earthquake,1.58,2.75,0.24,8,automatic,nc,nc
2022-01-17T07:28:34.434Z,-23.9653,-66.9681,235.44,4,mb,,62,1.501,0.55,us,us7000gcl0,2022-01-17T08:46:28.040Z,"71 km WNW of San Antonio de los Cobres, Argentina",earthquake,8.4,7.1,0.182,8,reviewed,us,us
2022-01-17T07:23:32.310Z,46.1965,-122.197166666667,3.85,0.09,md,10,176,0.005475,0.07,uw,uw61802202,2022-01-17T17:05:58.160Z,"37 km NNE of Amboy, Washington",earthquake,0.65,0.52,0.25463313640601,4,reviewed,uw,uw
2022-01-17T07:13:35.010Z,33.8766667,-116.9793333,14.67,1.07,ml,58,67,0.04462,0.16,ci,ci39914351,2022-01-18T21:29:20.920Z,"6km S of Beaumont, CA",earthquake,0.14,0.31,0.156,31,reviewed,ci,ci
2022-01-17T07:12:10.340Z,38.8318329,-122.8170013,1.9,0.86,md,19,52,0.01001,0.01,nc,nc73679566,2022-01-17T07:13:45.575Z,"8km NW of The Geysers, CA",earthquake,0.21,0.48,0.04,3,automatic,nc,nc
2022-01-17T07:10:01.538Z,60.676,-151.6572,67.5,1,ml,,,,0.47,ak,ak022s8d2wp,2022-01-17T07:17:36.465Z,"19 km WNW of Salamatof, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-17T07:06:16.520Z,58.4836666666667,-154.4155,4.03,0,ml,5,303,,0.21,av,av91047358,2022-01-19T23:14:22.670Z,"100 km WNW of Aleneva, Alaska",earthquake,1.18,1.51,0.118264246455576,5,reviewed,av,av
2022-01-17T07:00:43.314Z,61.4148,-148.1065,18.4,0.7,ml,,,,0.14,ak,ak022s8b0yz,2022-01-17T07:03:14.580Z,"43 km E of Knik River, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-17T06:46:44.340Z,33.7125,-116.7668333,15.95,0.52,ml,27,75,0.04392,0.09,ci,ci39914335,2022-01-18T21:18:51.614Z,"5km SW of Idyllwild, CA",earthquake,0.16,0.26,0.129,8,reviewed,ci,ci
2022-01-17T06:44:20.360Z,36.7695,-121.3081667,6.85,1.96,md,49,69,0.07531,0.09,nc,nc73679556,2022-01-17T20:35:13.094Z,"2km SSE of Tres Pinos, CA",earthquake,0.15,0.41,0.147,59,reviewed,nc,nc
2022-01-17T06:39:49.330Z,38.8276672,-122.8103333,0.94,0.85,md,9,164,0.004271,0.02,nc,nc73679551,2022-01-17T06:41:23.780Z,"7km NW of The Geysers, CA",earthquake,0.42,0.74,,1,automatic,nc,nc
2022-01-17T06:38:50.490Z,19.22483253479,-155.40983581543,33.9700012207031,1.85000002,md,43,139,,0.109999999,hv,hv72877947,2022-01-17T06:42:16.570Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.53,0.829999983,1.84000003,6,automatic,hv,hv
2022-01-17T06:37:38.907Z,58.4897,-154.4767,1.5,0.7,ml,,,,0.21,ak,ak022s7xiip,2022-01-19T18:10:39.870Z,"102 km N of Karluk, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-17T06:30:04.917Z,60.7501,-152.1578,84.9,1.3,ml,,,,0.61,ak,ak022s7vxvv,2022-01-17T06:34:50.969Z,"47 km W of Nikiski, Alaska",earthquake,,1.4,,,automatic,ak,ak
2022-01-17T06:28:43.160Z,38.841835,-122.8213348,1.53,0.86,md,11,101,0.01152,0.03,nc,nc73679546,2022-01-17T06:30:19.929Z,"9km WNW of Cobb, CA",earthquake,0.32,0.84,,1,automatic,nc,nc
2022-01-17T06:22:39.110Z,38.7801667,-122.9005,4.81,0.34,md,23,227,0.03584,0.04,nc,nc73679541,2022-01-22T01:56:48.873Z,"10km ESE of Cloverdale, CA",earthquake,0.38,0.44,0.085,3,reviewed,nc,nc
2022-01-17T06:21:41.786Z,60.819,-150.9829,19.8,1.2,ml,,,,0.55,ak,ak022s7u3aa,2022-01-17T06:25:29.691Z,"19 km SW of Point Possession, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-17T06:19:43.581Z,38.563,-119.521,6.5,1.1,ml,12,169.06,0.023,0.0987,nn,nn00831820,2022-01-17T06:24:27.455Z,"1 km WSW of Coleville, California",earthquake,,0.6,0.29,3,automatic,nn,nn
2022-01-17T06:15:45.672Z,59.7673,-150.9963,45.6,1.3,ml,,,,0.77,ak,ak022s7staf,2022-01-17T06:18:18.658Z,"10 km SSW of Fox River, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-17T06:12:21.700Z,46.872,-112.5253333,15.31,0.98,ml,8,171,0.049,0.09,mb,mb80536339,2022-01-18T21:18:47.680Z,"15 km SE of Lincoln, Montana",earthquake,1,0.6,0.515,2,reviewed,mb,mb
2022-01-17T06:04:44.447Z,36.6578,-116.2742,9.2,1.2,ml,15,82.36,0.053,0.1984,nn,nn00831817,2022-01-17T06:07:28.037Z,"51 km ESE of Beatty, Nevada",earthquake,,0.7,0.94,9,automatic,nn,nn
2022-01-17T06:04:33.470Z,40.2856667,-124.49,19.02,2.39,md,24,255,0.1128,0.07,nc,nc73679536,2022-01-18T08:31:10.836Z,"18km WSW of Petrolia, CA",earthquake,0.39,0.29,0.384,22,reviewed,nc,nc
2022-01-17T05:55:37.003Z,31.66454446,-104.3016918,6.774267578,2.2,ml,35,125,0.169772935,0.3,tx,tx2022bdru,2022-01-20T03:12:30.062Z,"57 km S of Whites City, New Mexico",earthquake,0.7464396765,1.290511956,0.2,19,reviewed,tx,tx
2022-01-17T05:53:31.678Z,38.1867,-117.8117,3.6,1.1,ml,12,158.16,0.126,0.1534,nn,nn00831815,2022-01-17T05:57:17.287Z,"34 km SE of Mina, Nevada",earthquake,,2.2,0.45,4,automatic,nn,nn
2022-01-17T05:46:50.620Z,38.2313333,-112.7651667,1.01,1.07,md,10,203,0.2012,0.06,uu,uu60477842,2022-01-18T17:01:36.910Z,"11 km WSW of Beaver, Utah",earthquake,0.92,6.71,0.045,6,reviewed,uu,uu
2022-01-17T05:41:24.340Z,19.1731662750244,-155.377838134766,36.0400009155273,1.75,md,14,218,,0.0900000036,hv,hv72877892,2022-01-17T05:44:36.220Z,"11 km ESE of Pāhala, Hawaii",earthquake,1.97,1.53999996,0.75,3,automatic,hv,hv
2022-01-17T05:40:56.410Z,58.4825,-154.81,6.11,-0.43,ml,7,106,,0.21,av,av91465306,2022-01-19T17:53:40.860Z,"103 km NNW of Karluk, Alaska",earthquake,0.44,1.53,0.216666763624961,7,reviewed,av,av
2022-01-17T05:40:27.438Z,62.8463,-151.2824,90.8,1.7,ml,,,,0.52,ak,ak022s7cp37,2022-01-17T05:47:05.101Z,"47 km NW of Petersville, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T05:35:55.310Z,38.8346672,-122.7788315,1.16,0.85,md,7,106,0.008129,0.01,nc,nc73679531,2022-01-17T05:37:29.180Z,"5km WNW of Cobb, CA",earthquake,0.66,1.02,,1,automatic,nc,nc
2022-01-17T05:35:17.630Z,47.4081666666667,-122.657666666667,22.48,0.92,ml,21,80,0.1262,0.17,uw,uw61802192,2022-01-17T16:55:05.690Z,"2 km WSW of Burley, Washington",earthquake,0.4,1.52,0.207988252445593,6,reviewed,uw,uw
2022-01-17T05:26:41.260Z,33.7135,-116.7651667,14.33,0.83,ml,30,65,0.04257,0.16,ci,ci39914319,2022-01-18T14:43:18.524Z,"5km SW of Idyllwild, CA",earthquake,0.26,0.36,0.192,28,reviewed,ci,ci
2022-01-17T05:24:32.000Z,33.7078333,-116.7718333,14.29,1.65,ml,58,22,0.04818,0.2,ci,ci39914311,2022-01-18T14:43:56.529Z,"6km SW of Idyllwild, CA",earthquake,0.2,0.37,0.237,27,reviewed,ci,ci
2022-01-17T05:19:31.100Z,19.1809997558594,-155.501007080078,31.0499992370605,1.85000002,md,28,198,,0.170000002,hv,hv72877877,2022-01-17T05:22:44.470Z,"3 km SW of Pāhala, Hawaii",earthquake,1.04,1.34000003,0.920000017,3,automatic,hv,hv
2022-01-17T05:19:04.207Z,62.422,-149.4958,65.7,1.6,ml,,,,0.84,ak,ak022s785cs,2022-01-17T05:29:12.864Z,"31 km E of Chase, Alaska",earthquake,,1.6,,,automatic,ak,ak
2022-01-17T05:16:15.140Z,38.7835007,-122.7433319,1.03,0.94,md,12,79,0.00517,0.04,nc,nc73679521,2022-01-17T05:17:53.521Z,"1km ENE of The Geysers, CA",earthquake,0.3,0.57,0.21,3,automatic,nc,nc
2022-01-17T05:10:52.120Z,45.487,-111.7455,5.45,0.07,ml,3,184,0.137,0.04,mb,mb80536314,2022-01-18T20:34:02.370Z,"15 km N of Ennis, Montana",earthquake,1.41,5.13,,0,reviewed,mb,mb
2022-01-17T05:09:36.920Z,38.8093333,-122.786,4.19,-0.09,md,4,231,0.007395,0.08,nc,nc73679516,2022-01-20T21:10:13.797Z,"4km NW of The Geysers, CA",earthquake,2.16,31.61,,1,reviewed,nc,nc
2022-01-17T05:03:53.410Z,19.22483253479,-155.427001953125,32.5900001525879,2.35,ml,48,129,,0.129999995,hv,hv72877852,2022-01-17T10:02:59.040Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.5,0.680000007,2.68,21,automatic,hv,hv
2022-01-17T04:59:32.155Z,-29.9563,-72.0921,10,4.6,mwr,,94,0.742,0.99,us,us7000gckp,2022-01-17T05:41:44.040Z,"72 km W of Coquimbo, Chile",earthquake,4.8,1.9,0.033,88,reviewed,us,us
2022-01-17T04:53:56.010Z,19.2238330841064,-155.426666259766,32.7400016784668,2.1400001,md,44,144,,0.140000001,hv,hv72877837,2022-01-17T04:57:14.390Z,"5 km ENE of Pāhala, Hawaii",earthquake,0.52,0.639999986,0.889999986,15,automatic,hv,hv
2022-01-17T04:42:55.478Z,60.7718,-150.783,49,1.3,ml,,,,0.34,ak,ak022s6rr63,2022-01-17T04:45:47.974Z,"Kenai Peninsula, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-17T04:37:35.110Z,33.3773333,-116.8815,7.18,1.25,ml,41,27,0.02844,0.23,ci,ci39914295,2022-01-18T14:43:56.794Z,"3km NW of Palomar Observatory, CA",earthquake,0.28,0.9,0.159,26,reviewed,ci,ci
2022-01-17T04:28:18.550Z,58.4865,-154.807,6.27,0,ml,7,110,,0.12,av,av91047353,2022-01-19T23:09:25.080Z,"104 km NNW of Karluk, Alaska",earthquake,0.32,1.02,0.11563431670586,7,reviewed,av,av
2022-01-17T04:26:53.904Z,59.8554,-152.9583,100.2,1,ml,,,,0.21,ak,ak022s6oc12,2022-01-17T04:45:47.825Z,"63 km W of Anchor Point, Alaska",earthquake,,1.5,,,automatic,ak,ak
2022-01-17T04:22:29.600Z,36.51833333,-99.2565,7,1.4,ml,26,212,0.1772652145,0.1,ok,ok2022bdos,2022-01-18T18:13:14.549Z,"9 km NNW of Mooreland, Oklahoma",earthquake,,0.3,0.16,8,reviewed,ok,ok
2022-01-17T04:09:51.680Z,51.8673333333333,-177.8565,3.79,0.79,ml,5,222,,0.07,av,av91465271,2022-01-19T17:51:10.050Z,"84 km W of Adak, Alaska",earthquake,0.66,0.58,0.356040808321877,5,reviewed,av,av
2022-01-17T04:08:23.030Z,33.595,-116.8083333,6.83,0.26,ml,18,77,0.03694,0.11,ci,ci39914287,2022-01-18T21:12:03.292Z,"13km WNW of Anza, CA",earthquake,0.24,0.41,0.096,6,reviewed,ci,ci
2022-01-17T04:05:34.652Z,58.0767,-154.446,4.9,1.7,ml,,,,0.51,ak,ak022s6js2h,2022-01-17T04:14:54.180Z,"56 km N of Karluk, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-17T04:05:15.970Z,17.9573,-66.9518,13,2.71,md,17,193,0.0747,0.11,pr,pr2022017000,2022-01-17T04:29:33.326Z,"4 km WSW of Guánica, Puerto Rico",earthquake,0.59,0.3,0.46,8,reviewed,pr,pr
2022-01-17T03:58:42.970Z,46.2003333333333,-122.191833333333,2.94,0.33,ml,13,127,0.0008753,0.11,uw,uw61802187,2022-01-17T16:34:06.050Z,"37 km NNE of Amboy, Washington",earthquake,0.39,0.51,0.0997240780304142,4,reviewed,uw,uw
2022-01-17T03:57:58.173Z,32.2377,137.762,377.46,4.2,mb,,161,1.939,0.76,us,us7000gckj,2022-01-17T04:08:00.040Z,"234 km SE of Shingū, Japan",earthquake,11.9,11.9,0.152,12,reviewed,us,us
2022-01-17T03:46:47.420Z,38.7766685,-122.7460022,1.55,0.9,md,15,88,0.009777,0.03,nc,nc73679511,2022-01-17T03:48:23.153Z,"1km E of The Geysers, CA",earthquake,0.28,0.52,0.14,4,automatic,nc,nc
2022-01-17T03:38:53.903Z,61.1722,-149.2093,31.2,1.3,ml,,,,0.74,ak,ak022s65gku,2022-01-17T03:42:20.153Z,"24 km ESE of Elmendorf Air Force Base, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-17T03:36:13.436Z,85.2101,91.82,10,4.8,mb,,65,11.648,0.6,us,us7000gcki,2022-01-17T04:56:34.040Z,"north of Severnaya Zemlya",earthquake,10.1,1.9,0.061,84,reviewed,us,us
2022-01-17T03:35:03.668Z,63.298,-151.2693,6.7,1.4,ml,,,,0.87,ak,ak022s64pjy,2022-01-17T03:42:20.002Z,"35 km SE of Denali National Park, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-17T03:31:53.117Z,85.2458,91.5293,10,4.9,mb,,39,11.618,0.57,us,us7000gckg,2022-01-17T03:56:18.040Z,"north of Severnaya Zemlya",earthquake,9.4,1.9,0.083,46,reviewed,us,us
2022-01-17T03:30:05.650Z,37.073,-121.5181667,3.22,1.09,md,24,50,0.0545,0.09,nc,nc73679501,2022-01-22T01:54:36.485Z,"8km E of San Martin, CA",earthquake,0.24,0.54,0.107,20,reviewed,nc,nc
2022-01-17T03:29:05.000Z,38.1133333,-112.6631667,5.9,1.18,md,7,251,0.2639,0.08,uu,uu60477837,2022-01-18T16:55:53.010Z,"18 km S of Beaver, Utah",earthquake,0.98,6.45,0.048,3,reviewed,uu,uu
2022-01-17T03:19:33.630Z,37.0326667,-121.4956667,8.63,1.69,md,57,44,0.01132,0.1,nc,nc73679496,2022-01-22T01:36:11.550Z,"7km ENE of Gilroy, CA",earthquake,0.16,0.32,0.214,51,reviewed,nc,nc
2022-01-17T02:55:08.060Z,40.2868333,-124.379,18.39,2.88,md,30,235,0.0279,0.09,nc,nc73679486,2022-01-18T23:48:07.040Z,"9km WSW of Petrolia, CA",earthquake,0.38,0.21,0.167,66,reviewed,nc,nc
2022-01-17T02:54:52.805Z,62.5081,-150.9338,73.8,1.8,ml,,,,0.47,ak,ak022s5ngch,2022-01-17T03:02:45.241Z,"8 km W of Petersville, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-17T02:50:47.158Z,38.1272,-117.9984,13.8,0.8,ml,9,145.31,0.033,0.2419,nn,nn00831814,2022-01-17T02:54:46.156Z,"30 km SSE of Mina, Nevada",earthquake,,0.8,0.49,4,automatic,nn,nn
2022-01-17T02:50:07.260Z,19.4213333129883,-155.39582824707,0.490000009536743,1.83,ml,42,44,,0.239999995,hv,hv72877687,2022-01-17T02:55:38.360Z,"17 km W of Volcano, Hawaii",earthquake,0.39,0.620000005,0.13,4,automatic,hv,hv
2022-01-17T02:40:14.810Z,38.8470001,-122.8188324,1.77,1.19,md,12,98,0.008423,0.01,nc,nc73679481,2022-01-17T03:29:11.823Z,"9km WNW of Cobb, CA",earthquake,0.3,0.72,,1,automatic,nc,nc
2022-01-17T02:38:02.130Z,36.1891667,-118.0265,2.57,0.89,ml,24,85,0.09759,0.15,ci,ci39914263,2022-01-18T21:02:00.003Z,"10km S of Olancha, CA",earthquake,0.21,0.77,0.141,10,reviewed,ci,ci
2022-01-17T02:37:06.290Z,33.7533333,-116.0363333,6.23,1.13,ml,27,138,0.108,0.14,ci,ci39914255,2022-01-18T20:11:54.972Z,"15km ENE of Coachella, CA",earthquake,0.27,0.71,0.159,14,reviewed,ci,ci
2022-01-17T02:23:58.380Z,37.4845,-118.8483333,1.36,0.84,md,17,207,0.1064,0.05,nc,nc73679476,2022-01-17T03:57:48.106Z,"17km WSW of Toms Place, CA",earthquake,0.4,31.61,0.146,14,reviewed,nc,nc
2022-01-17T02:22:03.140Z,19.1926670074463,-155.435333251953,32.4700012207031,1.80999994,md,17,156,,0.0900000036,hv,hv72877657,2022-01-17T02:25:06.010Z,"4 km ESE of Pāhala, Hawaii",earthquake,0.98,0.810000002,1.85000002,4,automatic,hv,hv
2022-01-17T02:21:49.700Z,35.11016667,-95.54916667,7.03,1.4,ml,35,83,0.112477928,0.28,ok,ok2022bdks,2022-01-18T17:57:20.226Z,"11 km E of Crowder, Oklahoma",earthquake,,0.9,0.27,7,reviewed,ok,ok
2022-01-17T02:15:55.840Z,38.8334999,-122.8205032,2.98,0.85,md,6,152,0.01276,0.02,nc,nc73679471,2022-01-17T02:17:33.065Z,"8km NW of The Geysers, CA",earthquake,1.03,2.88,,1,automatic,nc,nc
2022-01-17T02:12:26.200Z,37.0383333,-121.4898333,10.14,1.03,md,25,66,0.01352,0.09,nc,nc73679466,2022-01-17T19:39:07.090Z,"8km ENE of Gilroy, CA",earthquake,0.29,0.42,0.185,24,reviewed,nc,nc
2022-01-17T02:09:08.410Z,47.2123333,-113.2013333,6.45,0.58,md,5,196,0.148,0.03,mb,mb80536294,2022-01-18T18:53:12.730Z,"21 km E of Seeley Lake, Montana",earthquake,0.61,2.06,0.482,2,reviewed,mb,mb
2022-01-17T02:03:50.490Z,19.1591666666667,-155.484166666667,35.37,2.66,md,51,121,,0.1,hv,hv72877652,2022-01-18T20:17:19.620Z,"4 km S of Pāhala, Hawaii",earthquake,0.4,0.48,0.0969707128427679,20,reviewed,hv,hv
2022-01-17T02:03:48.990Z,38.8190002,-122.7606659,1.87,0.7,md,14,121,0.01354,0.02,nc,nc73679461,2022-01-17T02:05:23.904Z,"3km W of Cobb, CA",earthquake,0.31,0.59,0.16,2,automatic,nc,nc
2022-01-17T01:57:39.260Z,38.8226662,-122.8059998,2.15,0.71,md,15,67,0.003265,0.05,nc,nc73679456,2022-01-17T01:59:14.722Z,"7km NW of The Geysers, CA",earthquake,0.35,0.53,0.14,2,automatic,nc,nc
2022-01-17T01:54:27.360Z,37.0346667,-121.4926667,8.65,1.49,md,41,56,0.01119,0.13,nc,nc73679451,2022-01-22T01:01:11.205Z,"7km ENE of Gilroy, CA",earthquake,0.25,0.47,0.19,36,reviewed,nc,nc
2022-01-17T01:54:05.700Z,38.8230019,-122.8051682,2.16,0.99,md,23,42,0.003852,0.04,nc,nc73679446,2022-01-17T01:55:44.420Z,"7km NW of The Geysers, CA",earthquake,0.21,0.5,0.24,2,automatic,nc,nc
2022-01-17T01:51:06.018Z,63.5767,-149.9621,23.8,1.9,ml,,,,1.64,ak,ak022s519s0,2022-01-17T02:25:50.976Z,"54 km WNW of Cantwell, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T01:43:15.790Z,47.453,-115.7823333,0.16,1.64,ml,7,172,0.782,0.21,mb,mb80536284,2022-01-18T21:11:54.160Z,"northern Idaho",earthquake,1.19,6.91,0.076,2,reviewed,mb,mb
2022-01-17T01:30:38.230Z,37.4836667,-118.851,2.59,0.59,md,7,129,0.1076,0.03,nc,nc73679441,2022-01-17T01:50:38.241Z,"17km WSW of Toms Place, CA",earthquake,0.69,31.61,0.317,7,reviewed,nc,nc
2022-01-17T01:27:47.450Z,40.5075,-123.8973333,23.78,2.18,md,25,53,0.03844,0.08,nc,nc73679436,2022-01-19T11:20:10.851Z,"18km ESE of Hydesville, CA",earthquake,0.33,0.5,0.061,14,reviewed,nc,nc
2022-01-17T01:21:36.595Z,61.185,-144.0396,24.3,2,ml,,,,0.7,ak,ak022s4uwv6,2022-01-17T01:53:27.151Z,"42 km SSE of Chitina, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-17T01:20:20.840Z,57.5389,-155.2638,47.7,1.3,ml,,,,1.19,ak,ak022s4uob3,2022-01-19T17:45:43.660Z,"48 km W of Karluk, Alaska",earthquake,,2.1,,,automatic,ak,ak
2022-01-17T01:17:52.760Z,37.4878333,-118.8431667,3.55,1.16,md,17,267,0.1026,0.04,nc,nc73679431,2022-01-17T03:02:11.685Z,"17km WSW of Toms Place, CA",earthquake,0.5,1.57,0.075,12,reviewed,nc,nc
2022-01-17T01:16:59.420Z,38.8183327,-122.7975006,3.01,0.95,md,21,34,0.01049,0.02,nc,nc73679426,2022-01-17T01:18:33.235Z,"6km NW of The Geysers, CA",earthquake,0.25,0.5,0.06,4,automatic,nc,nc
2022-01-17T01:13:46.320Z,38.8190002,-122.7981644,2.82,0.5,md,22,50,0.01124,0.03,nc,nc73679421,2022-01-17T01:15:23.763Z,"6km NW of The Geysers, CA",earthquake,0.23,0.59,0.35,2,automatic,nc,nc
2022-01-17T01:12:58.010Z,46.8521666666667,-121.751333333333,1.76,0.34,ml,13,73,0.02079,0.08,uw,uw61802177,2022-01-17T16:25:40.130Z,"23 km ENE of Ashford, Washington",earthquake,0.2,0.51,0.181131577872212,7,reviewed,uw,uw
2022-01-17T01:07:15.630Z,38.788166,-122.7628326,1.29,0.46,md,9,83,0.01268,0.04,nc,nc73679416,2022-01-17T01:08:53.740Z,"1km NNW of The Geysers, CA",earthquake,0.33,0.75,0.4,2,automatic,nc,nc
2022-01-17T01:06:57.310Z,33.4571667,-116.5858333,11.5,0.87,ml,41,44,0.04074,0.16,ci,ci39914247,2022-01-18T19:58:09.454Z,"14km SE of Anza, CA",earthquake,0.17,0.45,0.189,22,reviewed,ci,ci
2022-01-17T01:00:51.730Z,38.8046684,-122.7813339,2.23,0.45,md,13,77,0.008593,0.02,nc,nc73679411,2022-01-17T01:02:28.225Z,"4km NW of The Geysers, CA",earthquake,0.29,0.56,0.39,2,automatic,nc,nc
2022-01-17T00:54:12.660Z,63.1911,-150.5601,123,2.1,ml,,,,0.41,ak,ak022s4gi3v,2022-01-17T01:23:13.013Z,"70 km SE of Denali National Park, Alaska",earthquake,,0.8,,,automatic,ak,ak
2022-01-17T00:51:19.260Z,34.0205,-117.1711667,7.17,0.96,ml,38,61,0.05103,0.17,ci,ci39914239,2022-01-18T19:45:47.922Z,"4km SSE of Redlands, CA",earthquake,0.22,0.48,0.121,21,reviewed,ci,ci
2022-01-17T00:50:04.090Z,35.8013333,-117.6153333,8.06,0.76,ml,12,104,0.02041,0.14,ci,ci39914231,2022-01-18T14:45:22.537Z,"19km WNW of Searles Valley, CA",earthquake,0.42,0.72,0.046,9,reviewed,ci,ci
2022-01-17T00:47:58.840Z,34.86433333,-97.82516667,7.69,1.05,ml,15,164,0.07828463788,0.3,ok,ok2022bdhq,2022-01-18T22:59:53.356Z,"7 km SW of Alex, Oklahoma",earthquake,,1.3,0.24,3,reviewed,ok,ok
2022-01-17T00:45:39.033Z,63.0347,-151.6915,11.5,1.6,ml,,,,0.76,ak,ak022s4emmn,2022-01-17T00:50:18.678Z,"56 km S of Denali National Park, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-17T00:27:39.130Z,34.85883333,-97.81316667,7,1.73,ml,19,99,0.0863830487,0.51,ok,ok2022bdgz,2022-01-18T17:22:53.610Z,"6 km SSW of Alex, Oklahoma",earthquake,,1.5,0.38,3,reviewed,ok,ok
2022-01-17T00:25:57.327Z,-7.5539,105.8746,35,5,mww,,48,1.762,1.7,us,us7000gcjn,2022-01-19T16:47:27.772Z,"97 km SW of Pelabuhanratu, Indonesia",earthquake,5,1.9,0.098,10,reviewed,us,us
2022-01-17T00:24:46.300Z,19.209,-155.414833333333,32.09,1.58,md,25,152,,0.12,hv,hv72877537,2022-01-19T03:13:47.170Z,"Island of Hawaii, Hawaii",earthquake,0.59,0.66,0.120189306647869,17,reviewed,hv,hv
2022-01-17T00:21:05.519Z,63.2213,-151.6528,14.2,2.7,ml,,,,0.97,ak,ak022s49eny,2022-01-17T00:34:56.774Z,"35 km S of Denali National Park, Alaska",earthquake,,0.6,,,automatic,ak,ak
2022-01-17T00:16:33.080Z,35.3308333,-118.5685,3.2,1.58,ml,30,45,0.1271,0.23,ci,ci39914207,2022-01-18T14:45:43.538Z,"25km NNW of Tehachapi, CA",earthquake,0.33,1.87,0.211,27,reviewed,ci,ci
2022-01-17T00:14:39.165Z,61.0664,-152.3076,93.7,1.8,ml,,,,0.81,ak,ak022s47zdg,2022-01-17T00:23:54.515Z,"63 km W of Tyonek, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-17T00:11:21.095Z,65.0014,-147.3913,4.8,1.8,ml,,,,0.83,ak,ak022s47auw,2022-01-17T00:18:13.547Z,"11 km ENE of Fox, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-17T00:02:29.990Z,34.4386667,-119.2985,10.42,3.19,ml,81,28,0.0416,0.33,ci,ci39914199,2022-01-22T07:02:42.123Z,"5km WSW of Ojai, CA",earthquake,0.26,0.52,0.15,145,reviewed,ci,ci
2022-01-17T00:01:21.850Z,35.8648333,-117.6671667,10.81,0.01,ml,8,94,0.07485,0.14,ci,ci37487725,2022-01-18T19:13:10.368Z,"23km ESE of Little Lake, CA",earthquake,0.4,0.98,0.037,5,reviewed,ci,ci
2022-01-17T00:00:57.400Z,35.862,-117.678,7.34,0.58,ml,14,85,0.08005,0.08,ci,ci39914191,2022-01-18T19:10:13.484Z,"22km ESE of Little Lake, CA",earthquake,0.17,0.46,0.16,6,reviewed,ci,ci
2022-01-16T23:52:56.950Z,58.2915,-154.820666666667,29.34,0.48,ml,10,192,,0.18,av,av91465186,2022-01-19T17:41:25.570Z,"83 km NNW of Karluk, Alaska",earthquake,0.72,0.79,0.311726405804126,10,reviewed,av,av
2022-01-16T23:42:16.556Z,62.3005,-148.3948,19.4,2.8,ml,,,,0.76,ak,ak022qujk6g,2022-01-17T00:10:48.040Z,"56 km N of Chickaloon, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-16T23:40:25.684Z,60.4909,-147.4226,19.1,2.5,ml,,,,0.84,ak,ak022quj5fx,2022-01-17T00:01:45.040Z,"57 km NE of Chenega, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-16T23:38:49.390Z,38.8294983,-122.8044968,1.56,0.85,md,8,89,0.007491,0.01,nc,nc73679396,2022-01-16T23:40:24.473Z,"7km W of Cobb, CA",earthquake,0.41,1.44,,1,automatic,nc,nc
2022-01-16T23:31:10.483Z,16.0347,-95.6864,35,5.3,mww,,89,3.149,1.19,us,us7000gcj6,2022-01-18T16:27:02.340Z,"2 km WNW of San Pedro Huamelula, Mexico",earthquake,8.7,1.9,0.06,27,reviewed,us,us
2022-01-16T23:21:24.900Z,40.434,-124.7273333,20.76,2.72,md,52,232,0.3004,0.19,nc,nc73679391,2022-01-19T12:46:10.384Z,"39km WNW of Petrolia, CA",earthquake,0.94,0.55,0.091,45,reviewed,nc,nc
2022-01-16T23:18:39.200Z,38.7873344,-122.7528305,0.47,0.95,md,15,80,0.01432,0.03,nc,nc73679386,2022-01-16T23:20:14.605Z,"1km NNE of The Geysers, CA",earthquake,0.24,0.53,0.19,3,automatic,nc,nc
2022-01-16T22:53:13.869Z,35.11116667,-95.53183333,7.2,1.52,ml,27,95,0.1043795172,0.21,ok,ok2022bddw,2022-01-18T17:03:20.560Z,"12 km E of Crowder, Oklahoma",earthquake,,0.7,0.24,9,reviewed,ok,ok
2022-01-16T22:50:48.590Z,38.75,-122.866,3.19,0.77,md,29,177,0.02416,0.07,nc,nc73679376,2022-01-20T22:31:52.447Z,"10km WSW of The Geysers, CA",earthquake,0.37,0.29,0.299,6,reviewed,nc,nc
2022-01-16T22:50:34.689Z,38.1326,-118.1565,0,0.9,ml,8,195.72,0.249,0.4317,nn,nn00831810,2022-01-16T22:54:26.542Z,"28 km S of Mina, Nevada",earthquake,,54,0.24,3,automatic,nn,nn
2022-01-16T22:48:38.245Z,38.1219,-118.157,12.1,1.9,ml,13,90.6,0.156,0.1458,nn,nn00831806,2022-01-18T18:58:09.928Z,"30 km S of Mina, Nevada",earthquake,,3.1,0.34,6,reviewed,nn,nn
2022-01-16T22:42:33.370Z,19.2080001831055,-155.519500732422,33.7700004577637,1.70000005,md,26,99,,0.100000001,hv,hv72877447,2022-01-16T22:45:51.060Z,"4 km W of Pāhala, Hawaii",earthquake,0.66,1.11000001,1.76999998,4,automatic,hv,hv
2022-01-16T22:42:10.179Z,57.0846,-156.0614,29.4,1.8,ml,,,,0.61,ak,ak022qty42h,2022-01-16T22:48:42.419Z,"93 km ESE of Ugashik, Alaska",earthquake,,1.4,,,automatic,ak,ak
2022-01-16T22:39:37.090Z,60.0258333333333,-153.065,-0.54,-0.77,ml,4,138,,0.05,av,av91465146,2022-01-19T16:53:59.140Z,"64 km ENE of Pedro Bay, Alaska",earthquake,0.36,2.88,0.405659184897829,4,reviewed,av,av
2022-01-16T22:38:10.490Z,38.7910004,-122.7666702,4.19,0.36,md,8,160,0.01675,0.02,nc,nc73679371,2022-01-16T22:39:50.160Z,"2km NNW of The Geysers, CA",earthquake,1.03,2.02,,1,automatic,nc,nc
2022-01-16T22:32:01.643Z,40.1168,24.4688,10,4.5,mb,,52,1.309,0.78,us,us7000gcj0,2022-01-20T05:57:58.040Z,"Aegean Sea",earthquake,2.9,1.9,0.18,9,reviewed,us,us
2022-01-16T22:31:13.880Z,38.844,-122.785,8.62,0.6,md,20,132,0.006861,0.1,nc,nc73679366,2022-01-22T00:34:41.456Z,"6km WNW of Cobb, CA",earthquake,0.9,1,0.16,5,reviewed,nc,nc
2022-01-16T22:28:17.200Z,19.4403324127197,-155.334335327148,3.50999999046326,1.70000005,md,21,70,,0.200000003,hv,hv72877427,2022-01-16T22:31:28.010Z,"10 km W of Volcano, Hawaii",earthquake,0.47,1.73000002,0.629999995,10,automatic,hv,hv
2022-01-16T22:16:17.473Z,36.2631,28.8646,44.67,4.1,mb,,107,0.599,0.99,us,us7000gciz,2022-01-20T05:53:09.392Z,"42 km SW of Ölüdeniz, Turkey",earthquake,3.2,11.2,0.107,24,reviewed,us,us
2022-01-16T22:14:52.550Z,38.8284988,-122.8044968,1.77,0.35,md,9,75,0.006705,0.01,nc,nc73679361,2022-01-16T22:16:28.368Z,"7km NW of The Geysers, CA",earthquake,0.43,1.38,,1,automatic,nc,nc
2022-01-16T22:05:09.480Z,38.8213348,-122.7916641,1.37,0.46,md,10,80,0.01177,0.03,nc,nc73679356,2022-01-16T22:06:42.715Z,"6km NNW of The Geysers, CA",earthquake,0.34,0.73,0.39,2,automatic,nc,nc
2022-01-16T22:04:49.797Z,43.7662,-98.3972,5,2.5,mb_lg,,53,0.787,0.48,us,us7000gciu,2022-01-20T05:44:26.040Z,"9 km NE of Plankinton, South Dakota",earthquake,2.1,2,0.228,5,reviewed,us,us
2022-01-16T22:04:17.500Z,19.3528333333333,-155.083333333333,6.57,3.5,ml,54,158,,0.12,hv,hv72877412,2022-01-20T05:30:46.513Z,"13 km SSE of Fern Forest, Hawaii",earthquake,0.47,0.34,0.117640936850649,37,reviewed,hv,hv
2022-01-16T22:01:05.640Z,38.8245,-122.7976667,2.74,0.04,md,21,33,0.009754,0.02,nc,nc73679351,2022-01-22T00:13:39.264Z,"6km NW of The Geysers, CA",earthquake,0.27,0.32,0.092,3,reviewed,nc,nc
2022-01-16T21:49:55.350Z,38.786499,-122.7320023,2.06,0.87,md,9,200,0.004923,0.02,nc,nc73679341,2022-01-16T21:51:34.156Z,"2km ENE of The Geysers, CA",earthquake,0.57,0.9,,1,automatic,nc,nc
2022-01-16T21:47:08.320Z,38.824,-122.7946667,3.2,0.28,md,19,35,0.01205,0.02,nc,nc73679331,2022-01-22T07:20:15.809Z,"6km NNW of The Geysers, CA",earthquake,0.28,0.51,0.261,4,reviewed,nc,nc
2022-01-16T21:39:31.210Z,59.9773333333333,-153.073,0.22,-0.87,ml,4,142,,0.07,av,av91465111,2022-01-19T16:44:45.300Z,"61 km ENE of Pedro Bay, Alaska",earthquake,0.27,1.39,0.169894042443887,4,reviewed,av,av
2022-01-16T21:30:20.240Z,32.7338333,-115.8365,8.18,1.18,ml,24,89,0.1124,0.22,ci,ci39914151,2022-01-18T21:43:56.350Z,"15km E of Ocotillo, CA",earthquake,0.29,1.15,0.193,9,reviewed,ci,ci
2022-01-16T21:25:34.920Z,60.0295,-153.101333333333,-0.69,-0.43,ml,4,190,,0.05,av,av91465096,2022-01-19T01:29:35.340Z,"62 km ENE of Pedro Bay, Alaska",earthquake,0.5,4.34,0.202601783037393,4,reviewed,av,av
2022-01-16T21:15:03.660Z,38.8245,-122.8041667,2.91,0.51,md,19,46,0.004744,0.02,nc,nc73679326,2022-01-20T21:03:43.564Z,"7km NW of The Geysers, CA",earthquake,0.22,0.32,0.044,2,reviewed,nc,nc
2022-01-16T21:14:00.230Z,19.2468338012695,-155.431167602539,31.3199996948242,2.04999995,md,33,118,,0.119999997,hv,hv72877347,2022-01-16T21:17:21.130Z,"6 km NE of Pāhala, Hawaii",earthquake,0.44,0.879999995,1.15999997,3,automatic,hv,hv
2022-01-16T21:10:19.700Z,46.1968333333333,-122.185833333333,2.61,0.42,ml,12,166,0.003375,0.14,uw,uw61802162,2022-01-17T15:53:11.950Z,"37 km NNE of Amboy, Washington",earthquake,0.54,0.77,0.35139554489725,4,reviewed,uw,uw
2022-01-16T21:04:52.100Z,38.836,-122.8178333,2,0.39,md,21,65,0.01397,0.02,nc,nc73679316,2022-01-22T06:28:41.183Z,"8km W of Cobb, CA",earthquake,0.23,0.41,0.43,2,reviewed,nc,nc
2022-01-16T21:04:19.760Z,36.8806667,-121.6171667,8.82,0.82,md,10,81,0.02056,0.07,nc,nc73679311,2022-01-22T20:39:53.071Z,"2km ESE of Aromas, CA",earthquake,0.33,0.35,0.174,7,reviewed,nc,nc
2022-01-16T20:42:31.480Z,38.7861671,-122.7344971,1.56,1.18,md,16,86,0.003405,0.04,nc,nc73679306,2022-01-16T21:15:11.872Z,"2km ENE of The Geysers, CA",earthquake,0.3,0.49,0.21,4,automatic,nc,nc
2022-01-16T20:29:01.310Z,33.5876667,-116.8081667,6.65,1.16,ml,42,40,0.05364,0.16,ci,ci39914111,2022-01-16T20:54:10.972Z,"13km WNW of Anza, CA",earthquake,0.18,0.4,0.179,28,reviewed,ci,ci
2022-01-16T20:25:05.205Z,61.4164,-150.0579,40.5,1.9,ml,,,,0.57,ak,ak022qsnla7,2022-01-16T20:29:06.923Z,"7 km NW of Point MacKenzie, Alaska",earthquake,,1.3,,,automatic,ak,ak
2022-01-16T20:24:05.200Z,38.8093338,-122.776001,-0.39,0.63,md,8,74,0.005362,0.03,nc,nc73679301,2022-01-16T20:25:42.478Z,"4km NNW of The Geysers, CA",earthquake,0.32,0.92,,1,automatic,nc,nc
2022-01-16T20:16:00.880Z,38.8175011,-122.7634964,1.8,0.91,md,14,113,0.01389,0.03,nc,nc73679296,2022-01-16T20:17:37.831Z,"4km W of Cobb, CA",earthquake,0.28,0.48,0.25,3,automatic,nc,nc
2022-01-16T20:08:33.580Z,38.8066673,-122.7641678,-0.06,0.4,md,7,93,0.006966,0.03,nc,nc73679286,2022-01-16T20:10:08.155Z,"3km NNW of The Geysers, CA",earthquake,0.36,0.64,0.28,2,automatic,nc,nc
2022-01-16T20:06:52.030Z,36.53866667,-98.95616667,6.86,0.86,ml,17,116,0.04589099462,0.07,ok,ok2022bcyj,2022-01-18T16:52:39.276Z,"8 km SW of Waynoka, Oklahoma",earthquake,,0.3,0.27,4,reviewed,ok,ok
2022-01-16T20:04:23.993Z,60.9097,-147.3489,0.8,2,ml,,,,0.93,ak,ak022qsj4py,2022-01-16T20:25:16.108Z,"36 km W of Tatitlek, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-16T19:59:53.530Z,36.53766667,-98.9545,6.58,1.25,ml,17,115,0.04409134777,0.05,ok,ok2022bcyd,2022-01-18T16:27:50.453Z,"8 km SW of Waynoka, Oklahoma",earthquake,,0.2,0.28,4,reviewed,ok,ok
2022-01-16T19:57:29.783Z,62.8555,-151.3602,107.2,1.8,ml,,,,0.28,ak,ak022qs92hw,2022-01-16T20:04:42.119Z,"50 km NW of Petersville, Alaska",earthquake,,0.7,,,automatic,ak,ak
2022-01-16T19:52:04.276Z,61.5841,-151.1337,91.8,1.6,ml,,,,0.63,ak,ak022qs7xyj,2022-01-16T19:55:00.275Z,"33 km W of Susitna, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-16T19:05:52.960Z,33.4788333,-116.4301667,12.62,1.32,ml,48,36,0.04461,0.19,ci,ci39914103,2022-01-16T20:55:40.390Z,"23km SSW of La Quinta, CA",earthquake,0.25,0.48,0.155,27,reviewed,ci,ci
2022-01-16T19:05:05.900Z,37.4698333,-118.8115,4.03,1,md,22,133,0.11,0.03,nc,nc73679271,2022-01-16T21:31:48.481Z,"16km SW of Toms Place, CA",earthquake,0.28,1.38,0.106,20,reviewed,nc,nc
2022-01-16T18:43:20.020Z,19.1895,-155.4795,34.68,1.46,md,20,152,,0.1,hv,hv72877172,2022-01-18T21:12:52.740Z,"1 km S of Pāhala, Hawaii",earthquake,0.58,0.59,0.00841117585857609,7,reviewed,hv,hv
2022-01-16T18:40:55.990Z,33.5873333,-116.8058333,7.16,1.03,ml,38,39,0.05511,0.17,ci,ci39914079,2022-01-16T20:55:45.240Z,"13km WNW of Anza, CA",earthquake,0.22,0.6,0.19,28,reviewed,ci,ci
2022-01-16T18:31:28.510Z,44.7758333,-110.8096667,7.69,1.24,md,11,118,0.09019,0.1,uu,uu60477817,2022-01-18T14:22:25.800Z,"23 km SSW of Mammoth, Wyoming",earthquake,0.33,0.62,0.178,6,reviewed,uu,uu
2022-01-16T18:29:27.882Z,40.0303,24.3601,10,4.2,mb,,48,1.428,0.77,us,us7000gci5,2022-01-16T20:59:12.040Z,"27 km SSE of Karyes, Greece",earthquake,4.2,2,0.215,6,reviewed,us,us
2022-01-16T18:21:42.070Z,60.0271666666667,-153.102166666667,0.31,-0.72,ml,5,187,,0.08,av,av91465016,2022-01-19T01:24:43.810Z,"Southern Alaska",earthquake,0.48,0.93,0.215718708720167,5,reviewed,av,av
2022-01-16T18:17:59.679Z,64.9549,-146.3297,0,2.2,ml,,,,0.98,ak,ak022qrf4ks,2022-01-16T19:31:47.648Z,"26 km ENE of Pleasant Valley, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-16T18:17:04.378Z,31.65995862,-104.445905,5.643115234,2.2,ml,24,73,0.04757031219,0.2,tx,tx2022bcus,2022-01-18T02:21:25.669Z,"57 km S of Whites City, New Mexico",earthquake,1.385839211,1.716593261,0.1,11,reviewed,tx,tx
2022-01-16T18:10:36.980Z,65.0267,-147.1468,12.3,1.4,ml,,,,0.79,ak,ak022qrdksy,2022-01-16T18:13:28.099Z,"17 km NNW of Two Rivers, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-16T18:09:35.200Z,36.53916667,-98.95633333,7.12,1.72,ml,26,111,0.04679081805,0.08,ok,ok2022bcum,2022-01-18T23:06:51.211Z,"8 km SW of Waynoka, Oklahoma",earthquake,,0.2,0.22,4,reviewed,ok,ok
2022-01-16T18:08:36.740Z,40.4545,-124.4821667,19.66,2.34,md,28,234,0.1124,0.1,nc,nc73679266,2022-01-18T07:58:19.632Z,"22km NW of Petrolia, CA",earthquake,0.5,0.28,0.372,25,reviewed,nc,nc
2022-01-16T18:05:24.757Z,60.0375,-153.2408,122.1,2.2,ml,,,,0.51,ak,ak022qrcha5,2022-01-16T21:07:07.040Z,"55 km ENE of Pedro Bay, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-16T17:56:34.449Z,61.2206,-150.8126,49.8,1.5,ml,,,,0.67,ak,ak022qr1zwl,2022-01-16T18:00:56.190Z,"17 km ENE of Beluga, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-16T17:55:41.170Z,19.3441666666667,-155.139,7.23,0.66,md,17,116,,0.09,hv,hv72877132,2022-01-16T19:58:32.330Z,"13 km S of Fern Forest, Hawaii",earthquake,0.43,0.88,0.0564626479041374,7,reviewed,hv,hv
2022-01-16T17:49:03.630Z,37.497,-118.8503333,0.26,0.21,md,8,326,0.09438,0.05,nc,nc73679261,2022-01-16T21:22:47.172Z,"17km WSW of Toms Place, CA",earthquake,1.35,31.61,0.239,8,reviewed,nc,nc
2022-01-16T17:43:56.056Z,60.4895,-151.3775,21,1.1,ml,,,,0.16,ak,ak022qqz9at,2022-01-16T17:51:04.790Z,"9 km NNW of Kalifornsky, Alaska",earthquake,,7.2,,,automatic,ak,ak
2022-01-16T17:40:37.150Z,31.62301124,-104.105251,7.468383789,2.3,ml,32,59,0.07629700299,0.3,tx,tx2022bctn,2022-01-18T02:07:00.069Z,"45 km NW of Toyah, Texas",earthquake,1.178782951,0.8959834096,0.2,16,reviewed,tx,tx
2022-01-16T17:37:42.070Z,38.757,-122.73,2.32,0.11,md,19,112,0.006097,0.04,nc,nc73679256,2022-01-22T00:09:08.737Z,"3km SE of The Geysers, CA",earthquake,0.23,0.3,0.174,3,reviewed,nc,nc
2022-01-16T17:35:10.460Z,35.752,-117.5406667,6.75,1.14,ml,16,151,0.07862,0.16,ci,ci39914047,2022-01-16T20:55:14.519Z,"12km W of Searles Valley, CA",earthquake,0.45,0.93,0.235,11,reviewed,ci,ci
2022-01-16T17:30:10.457Z,60.3745,-150.7755,45.9,1.4,ml,,,,0.25,ak,ak022qqwdh1,2022-01-16T17:33:12.466Z,"14 km S of Funny River, Alaska",earthquake,,1.7,,,automatic,ak,ak
2022-01-16T17:23:26.750Z,39.2431667,-123.1833333,5.91,1.16,md,7,278,0.09881,0.06,nc,nc73679251,2022-01-16T22:33:11.875Z,"3km SE of Redwood Valley, CA",earthquake,3.12,1.72,0.154,7,reviewed,nc,nc
2022-01-16T17:05:16.170Z,38.75,-122.6888351,-0.67,0.68,md,7,197,0.0199,0.03,nc,nc73679241,2022-01-16T17:06:53.651Z,"3km S of Anderson Springs, CA",earthquake,0.47,1.58,0.16,2,automatic,nc,nc
2022-01-16T16:53:05.110Z,60.0245,-153.092166666667,-1.81,-0.33,ml,5,114,,0.04,av,av91464936,2022-01-19T01:11:23.500Z,"Southern Alaska",earthquake,0.23,3.79,0.161374047445647,5,reviewed,av,av
2022-01-16T16:51:26.570Z,33.6073333,-116.7058333,2.61,0.4,ml,15,68,0.04939,0.1,ci,ci39914023,2022-01-18T16:25:29.694Z,"6km NNW of Anza, CA",earthquake,0.17,0.28,0.033,4,reviewed,ci,ci
2022-01-16T16:51:00.640Z,38.7750015,-122.7136688,1.66,0.68,md,9,93,0.01315,0.01,nc,nc73679236,2022-01-16T16:52:36.770Z,"2km W of Anderson Springs, CA",earthquake,0.31,0.5,0.26,3,automatic,nc,nc
2022-01-16T16:36:43.903Z,-15.1799,-72.3231,111.16,4.4,mb,,258,3.631,0.75,us,us7000gchh,2022-01-16T17:02:17.040Z,"9 km NNE of Orcopampa, Peru",earthquake,12,18.4,0.179,9,reviewed,us,us
2022-01-16T16:35:05.912Z,65.2156,-146.4989,11.6,1.7,ml,,,,0.52,ak,ak022qqc04a,2022-01-16T16:41:34.225Z,"41 km NNE of Pleasant Valley, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-16T16:35:00.644Z,59.6339,-152.2465,85.7,1.5,ml,,,,0.6,ak,ak022qqbzow,2022-01-16T16:38:13.575Z,"28 km SW of Anchor Point, Alaska",earthquake,,1.1,,,automatic,ak,ak
2022-01-16T16:28:51.590Z,19.1653327941895,-155.477493286133,34.75,2.15,ml,48,101,,0.119999997,hv,hv72877077,2022-01-16T16:34:22.360Z,"4 km S of Pāhala, Hawaii",earthquake,0.57,0.730000019,3.98,3,automatic,hv,hv
2022-01-16T16:26:21.530Z,37.4815,-118.8546667,2.92,0.61,md,13,238,0.1102,0.08,nc,nc73679231,2022-01-16T21:13:15.940Z,"18km WSW of Toms Place, CA",earthquake,0.89,2.87,0.142,12,reviewed,nc,nc
2022-01-16T16:20:59.910Z,37.4845,-118.8398333,4.15,1.71,md,24,129,0.1057,0.05,nc,nc73679226,2022-01-16T21:41:11.579Z,"16km WSW of Toms Place, CA",earthquake,0.26,1.12,0.144,22,reviewed,nc,nc
2022-01-16T16:14:32.119Z,34.90383333,-98.001,6,1.47,ml,8,136,0.1304743965,0.44,ok,ok2022bcqs,2022-01-18T16:14:23.748Z,"8 km SW of Ninnekah, Oklahoma",earthquake,,3,0.42,3,reviewed,ok,ok
2022-01-16T16:07:31.320Z,38.8455009,-122.8166656,1.39,0.86,md,9,84,0.01053,0.01,nc,nc73679221,2022-01-16T16:09:07.891Z,"8km WNW of Cobb, CA",earthquake,0.31,0.88,,1,automatic,nc,nc
2022-01-16T15:49:20.230Z,18.9156,-64.9036,41,3.62,md,14,318,0.7165,0.5,pr,pr2022016008,2022-01-16T17:06:39.179Z,"63 km N of Charlotte Amalie, U.S. Virgin Islands",earthquake,5.24,14.04,0.14,8,reviewed,pr,pr
2022-01-16T15:45:24.140Z,19.4083333333333,-155.268166666667,2.68,0.46,md,20,52,,0.09,hv,hv72877017,2022-01-16T18:42:20.300Z,"5 km SW of Volcano, Hawaii",earthquake,0.24,0.31,0.0938375617398716,5,reviewed,hv,hv
2022-01-16T15:43:35.335Z,62.2556,-150.8796,63.7,1.5,ml,,,,0.65,ak,ak022qpscho,2022-01-16T15:48:28.140Z,"27 km SSW of Petersville, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-16T15:35:31.840Z,19.1176666666667,-155.458,29.33,1.52,md,39,227,,0.14,hv,hv72877012,2022-01-19T02:38:00.530Z,"9 km SSE of Pāhala, Hawaii",earthquake,0.48,0.56,0.0732924914324029,18,reviewed,hv,hv
2022-01-16T15:32:34.697Z,-17.4266,-174.2131,131.58,4.6,mb,,72,4.874,0.47,us,us7000gchb,2022-01-17T13:36:09.358Z,"137 km N of Neiafu, Tonga",earthquake,10.5,7.1,0.067,66,reviewed,us,us
2022-01-16T15:28:30.360Z,38.8289986,-122.8138351,1.79,0.89,md,23,44,0.00632,0.02,nc,nc73679216,2022-01-16T15:30:06.106Z,"8km NW of The Geysers, CA",earthquake,0.19,0.39,0.2,4,automatic,nc,nc
2022-01-16T15:24:39.842Z,60.1736,-153.2869,143.5,2.1,ml,,,,0.87,ak,ak022qpoa7s,2022-01-16T15:29:35.796Z,"57 km E of Port Alsworth, Alaska",earthquake,,0.4,,,automatic,ak,ak
2022-01-16T15:08:14.960Z,38.7868347,-122.7679977,2.28,0.99,md,16,81,0.01522,0.03,nc,nc73679206,2022-01-16T15:09:51.948Z,"2km NW of The Geysers, CA",earthquake,0.28,0.57,0.16,3,automatic,nc,nc
2022-01-16T15:06:21.503Z,56.7472,-155.8132,22.4,3.4,ml,,,,0.86,ak,ak022qpkdsl,2022-01-16T22:05:28.040Z,"102 km WSW of Akhiok, Alaska",earthquake,,2.3,,,reviewed,ak,ak
2022-01-16T15:05:13.272Z,38.385,-118.2107,5.7,1.4,ml,8,94.63,0.063,0.0235,nn,nn00831803,2022-01-21T00:54:29.355Z,"California-Nevada border region",earthquake,,3,0.32,2,reviewed,nn,nn
2022-01-16T15:00:16.300Z,19.4106666666667,-155.2615,1.17,2.14,md,20,76,,0.14,hv,hv72876992,2022-01-16T18:29:11.330Z,"4 km SW of Volcano, Hawaii",earthquake,0.22,0.26,0.0269807102691404,6,reviewed,hv,hv
2022-01-16T14:59:50.590Z,35.97,-117.3875,2.97,2.45,ml,37,63,0.1156,0.14,ci,ci39913999,2022-01-18T21:59:17.040Z,"23km N of Searles Valley, CA",earthquake,0.17,0.56,0.127,24,reviewed,ci,ci
2022-01-16T14:58:38.930Z,46.5698333333333,-121.738,-0.93,1.28,ml,30,139,0.1803,0.19,uw,uw61802142,2022-01-16T16:17:35.810Z,"6 km SW of Packwood, Washington",earthquake,0.46,1.22,0.171293157973702,10,reviewed,uw,uw
2022-01-16T14:48:17.520Z,35.9726667,-117.39,2.86,1.21,ml,19,161,0.1189,0.12,ci,ci39913983,2022-01-18T21:21:03.057Z,"23km N of Searles Valley, CA",earthquake,0.25,0.84,0.212,6,reviewed,ci,ci
2022-01-16T14:47:38.160Z,33.7163333,-116.8243333,17.22,0.75,ml,23,96,0.0883,0.11,ci,ci39913975,2022-01-16T16:22:35.302Z,"7km ESE of Valle Vista, CA",earthquake,0.26,0.39,0.241,8,reviewed,ci,ci
2022-01-16T14:40:38.709Z,62.7928,-148.9488,58.4,1.9,ml,,,,0.88,ak,ak022qp69zx,2022-01-16T14:44:50.326Z,"66 km S of Cantwell, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-16T14:34:35.612Z,60.1013,-148.3864,14.3,3.4,ml,,,,0.94,ak,ak022qp4zgo,2022-01-16T22:00:09.040Z,"21 km W of Chenega, Alaska",earthquake,,0.3,,,reviewed,ak,ak
2022-01-16T14:27:08.050Z,46.9136667,-112.5085,10.52,1.49,ml,19,73,0.065,0.16,mb,mb80536174,2022-01-18T21:11:10.120Z,"Western Montana",earthquake,0.38,0.6,0.197,5,reviewed,mb,mb
2022-01-16T14:11:23.280Z,19.409,-155.267833333333,1.28,0.26,md,9,88,,0.09,hv,hv72876942,2022-01-16T18:49:48.760Z,"Island of Hawaii, Hawaii",earthquake,0.3,0.42,0.0415318014380279,3,reviewed,hv,hv
2022-01-16T14:07:22.324Z,61.5684,-141.0545,16.5,1.6,ml,,,,0.42,ak,ak022qoz63s,2022-01-16T14:10:25.588Z,"Southern Alaska",earthquake,,1.2,,,automatic,ak,ak
2022-01-16T14:00:05.390Z,19.412,-155.270166666667,2.12,0.32,md,13,66,,0.09,hv,hv72876927,2022-01-16T18:57:11.710Z,"5 km SW of Volcano, Hawaii",earthquake,0.29,0.44,0.00408744279943418,3,reviewed,hv,hv
2022-01-16T13:59:33.430Z,38.8303333,-122.8546667,1.54,0.04,md,18,71,0.003274,0.06,nc,nc73679196,2022-01-22T00:01:06.919Z,"10km NW of The Geysers, CA",earthquake,0.27,0.33,0.151,2,reviewed,nc,nc
2022-01-16T13:58:43.820Z,19.1431,-68.1741,10,3.32,md,17,193,0.6625,0.76,pr,pr2022016006,2022-01-16T16:30:49.040Z,"66 km NNE of Punta Cana, Dominican Republic",earthquake,4.4,31.61,0.19,10,reviewed,pr,pr
2022-01-16T13:55:46.380Z,38.5866667,-122.7551667,7.19,1.01,md,35,65,0.0964,0.08,nc,nc73679191,2022-01-17T19:28:36.585Z,"7km NE of Windsor, CA",earthquake,0.2,0.75,0.237,15,reviewed,nc,nc
2022-01-16T13:52:30.750Z,19.415,-155.270833333333,2.23,0.3,md,12,56,,0.09,hv,hv72876917,2022-01-16T19:05:25.920Z,"4 km SW of Volcano, Hawaii",earthquake,0.32,0.5,0.0306287355518553,4,reviewed,hv,hv
2022-01-16T13:50:17.760Z,33.1448333,-116.915,14.34,0.96,ml,37,53,0.1297,0.19,ci,ci39913967,2022-01-18T21:13:27.260Z,"7km NNE of San Pasqual, CA",earthquake,0.21,0.62,0.142,18,reviewed,ci,ci
2022-01-16T13:49:26.710Z,46.195,-122.185833333333,0.98,1.03,ml,11,172,0.005206,0.09,uw,uw61802132,2022-01-16T17:26:56.310Z,"37 km NNE of Amboy, Washington",earthquake,0.45,0.38,0.186518089255237,2,reviewed,uw,uw
2022-01-16T13:43:14.639Z,45.6552,26.5828,141.36,4.3,mb,,43,0.477,0.88,us,us7000gcgw,2022-01-17T00:52:08.446Z,"10 km WSW of Nereju Mic, Romania",earthquake,6.9,3.9,0.091,35,reviewed,us,us
2022-01-16T13:42:31.473Z,59.6801,-152.7894,88.7,2.1,ml,,,,0.45,ak,ak022qol98p,2022-01-16T15:12:26.040Z,"54 km WSW of Anchor Point, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-16T13:36:57.687Z,40.1069,24.3926,10,4,mb,,58,1.353,0.81,us,us7000gcgt,2022-01-16T15:06:08.040Z,"20 km SE of Karyes, Greece",earthquake,3.9,2,0.365,2,reviewed,us,us
2022-01-16T13:33:12.770Z,19.1504993438721,-155.467498779297,33.2599983215332,1.85000002,md,41,169,,0.109999999,hv,hv72876882,2022-01-16T13:36:32.100Z,"Island of Hawaii, Hawaii",earthquake,0.56,0.75999999,0.879999995,7,automatic,hv,hv
2022-01-16T13:29:43.440Z,46.8968333333333,-121.892,6.24,0.92,ml,17,100,0.03646,0.09,uw,uw61802127,2022-01-16T16:26:27.860Z,"18 km NE of Ashford, Washington",earthquake,0.24,0.48,0.23795175835149,8,reviewed,uw,uw
2022-01-16T13:29:03.806Z,59.8711,-152.5425,61.6,2,ml,,,,0.68,ak,ak022qoiequ,2022-01-16T13:40:31.563Z,"41 km WNW of Anchor Point, Alaska",earthquake,,0.5,,,automatic,ak,ak
2022-01-16T13:23:54.550Z,19.4145,-155.259666666667,1.21,0.57,md,19,96,,0.14,hv,hv72876867,2022-01-16T19:13:43.670Z,"4 km SW of Volcano, Hawaii",earthquake,0.22,0.3,0.0734494070035456,5,reviewed,hv,hv
2022-01-16T13:23:26.960Z,36.5585,-121.1528333,7.92,1.87,md,37,64,0.02801,0.06,nc,nc73679186,2022-01-21T23:23:13.218Z,"3km NNW of Pinnacles, CA",earthquake,0.2,0.33,0.219,37,reviewed,nc,nc
2022-01-16T13:14:22.080Z,38.756,-122.7238333,1.43,0.26,md,10,112,0.005642,0.03,nc,nc73679181,2022-01-20T20:49:41.678Z,"4km SW of Anderson Springs, CA",earthquake,0.31,0.39,0.122,3,reviewed,nc,nc
2022-01-16T13:11:37.320Z,19.1483325958252,-155.449661254883,32.8800010681152,1.94000006,md,38,173,,0.129999995,hv,hv72876857,2022-01-16T13:14:54.050Z,"6 km SSE of Pāhala, Hawaii",earthquake,0.6,0.720000029,1.94000006,4,automatic,hv,hv
2022-01-16T13:08:20.650Z,19.1861667633057,-155.483993530273,37.1599998474121,2.44000006,md,52,73,,0.119999997,hv,hv72876852,2022-01-16T13:13:51.240Z,"1 km SSW of Pāhala, Hawaii",earthquake,0.46,0.610000014,1.98000002,30,automatic,hv,hv
2022-01-16T13:08:04.560Z,19.4741666666667,-155.22,23.01,1.1,md,16,163,,0.13,hv,hv72876842,2022-01-18T23:00:39.570Z,"3 km NNE of Volcano, Hawaii",earthquake,0.84,0.64,0.0251003344123367,6,reviewed,hv,hv
2022-01-16T13:02:24.820Z,19.4156666666667,-155.271333333333,2.39,0.33,md,16,57,,0.1,hv,hv72876832,2022-01-16T19:36:44.410Z,"4 km SW of Volcano, Hawaii",earthquake,0.27,0.35,0.040432621955049,4,reviewed,hv,hv
2022-01-16T12:55:52.760Z,35.8651667,-117.662,10.57,0.57,ml,10,99,0.07196,0.09,ci,ci39913951,2022-01-18T21:04:58.948Z,"23km ESE of Little Lake, CA",earthquake,0.25,0.44,0.141,4,reviewed,ci,ci
2022-01-16T12:54:41.890Z,19.2103328704834,-155.419998168945,32.5400009155273,1.88999999,md,21,202,,0.100000001,hv,hv72876822,2022-01-16T12:57:47.890Z,"6 km E of Pāhala, Hawaii",earthquake,1,0.769999981,0.629999995,3,automatic,hv,hv
2022-01-16T12:52:39.910Z,19.4116666666667,-155.27,1.48,0.29,md,12,64,,0.08,hv,hv72876812,2022-01-16T19:43:03.580Z,"5 km SW of Volcano, Hawaii",earthquake,0.21,0.41,0.0448230856945123,4,reviewed,hv,hv
2022-01-16T12:52:10.596Z,-6.4459,154.8206,408.08,6.1,mww,,20,5.884,0.63,us,us7000gcfv,2022-01-17T21:18:26.040Z,"74 km W of Panguna, Papua New Guinea",earthquake,9.5,6.1,0.049,40,reviewed,us,us
2022-01-16T12:49:30.000Z,35.6605,-117.488,8.44,2.19,ml,25,87,0.07677,0.15,ci,ci39913943,2022-01-16T14:43:21.740Z,"14km SSW of Searles Valley, CA",earthquake,0.28,0.82,0.124,26,reviewed,ci,ci
2022-01-16T12:48:39.635Z,37.4573,-117.9454,0,1.7,ml,12,121.65,0.327,0.318,nn,nn00831790,2022-01-20T01:39:21.010Z,"25 km SSE of Dyer, Nevada",earthquake,,0,0.33,4,reviewed,nn,nn
2022-01-16T12:36:33.120Z,17.893,-65.7081,10,3.59,md,20,226,0.2566,0.67,pr,pr2022016007,2022-01-16T16:23:57.334Z,"21 km ESE of Emajagua, Puerto Rico",earthquake,2.28,31.61,0.04,13,reviewed,pr,pr
2022-01-16T12:26:18.241Z,40.0695,24.3299,10,4.6,mb,,35,1.412,0.56,us,us7000gcfr,2022-01-16T12:43:24.040Z,"22 km SSE of Karyes, Greece",earthquake,5.3,1.9,0.122,20,reviewed,us,us
2022-01-16T12:15:21.310Z,33.8943333,-116.8455,15.29,0.79,ml,31,57,0.07263,0.15,ci,ci39913927,2022-01-18T20:59:07.921Z,"4km SE of Banning, CA",earthquake,0.22,0.5,0.144,20,reviewed,ci,ci
2022-01-16T12:10:41.820Z,37.5,-118.8486667,2.34,0.25,md,7,236,0.0912,0.03,nc,nc73679171,2022-01-16T19:59:10.824Z,"16km WSW of Toms Place, CA",earthquake,0.97,3.06,0.308,7,reviewed,nc,nc
2022-01-16T11:57:24.790Z,38.8266678,-122.8508301,-0.68,0.86,md,8,75,0.01284,0.05,nc,nc73679166,2022-01-16T11:59:02.303Z,"10km NW of The Geysers, CA",earthquake,0.27,1.89,,1,automatic,nc,nc
2022-01-16T11:54:47.289Z,34.86666667,-97.82466667,6.68,1.41,ml,23,63,0.07558516761,0.2,ok,ok2022bcid,2022-01-18T15:06:15.473Z,"6 km SW of Alex, Oklahoma",earthquake,,0.6,0.22,8,reviewed,ok,ok
2022-01-16T11:48:05.595Z,40.0353,24.3694,9.29,5.5,mww,,19,1.42,0.55,us,us7000gcfq,2022-01-19T20:51:05.040Z,"26 km SSE of Karyes, Greece",earthquake,5.5,3.7,0.049,40,reviewed,us,us
2022-01-16T11:30:59.490Z,38.7910004,-122.8054962,3.44,0.49,md,11,93,0.003275,0.02,nc,nc73679161,2022-01-16T11:32:36.724Z,"4km WNW of The Geysers, CA",earthquake,0.43,1.15,0.35,2,automatic,nc,nc
2022-01-16T11:21:42.090Z,19.2140007019043,-155.412826538086,35.0400009155273,2.02999997,md,39,144,,0.119999997,hv,hv72876752,2022-01-16T11:24:48.960Z,"7 km E of Pāhala, Hawaii",earthquake,0.5,0.74000001,1.61000001,14,automatic,hv,hv
2022-01-16T11:15:21.792Z,63.2135,-150.9247,0,1.9,ml,,,,1.23,ak,ak022qn8kyv,2022-01-16T12:02:40.163Z,"54 km SE of Denali National Park, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-16T11:03:26.670Z,38.7856674,-122.7506638,0.74,0.98,md,13,87,0.01116,0.04,nc,nc73679156,2022-01-16T11:05:01.577Z,"1km NNE of The Geysers, CA",earthquake,0.29,0.66,0.06,3,automatic,nc,nc
2022-01-16T10:57:40.429Z,36.76,-98.06716667,7.26,2.03,ml,82,112,0.09988040006,0.22,ok,ok2022bcgf,2022-01-18T14:23:36.053Z,"7 km E of Nescatunga, Oklahoma",earthquake,,0.5,0.3,5,reviewed,ok,ok
2022-01-16T10:47:23.480Z,33.2065,-116.0098333,6.99,0.86,ml,33,62,0.0761,0.19,ci,ci39913919,2022-01-18T20:49:54.863Z,"11km SSW of Salton City, CA",earthquake,0.23,0.74,0.086,10,reviewed,ci,ci
2022-01-16T10:40:16.750Z,34.3656667,-119.4575,3.99,1.46,ml,24,178,0.0587,0.25,ci,ci39913911,2022-01-18T20:39:43.812Z,"7km ESE of Carpinteria, CA",earthquake,0.51,1.07,0.138,13,reviewed,ci,ci
2022-01-16T10:36:04.260Z,38.8101667,-122.7775,-0.47,0.42,md,8,108,0.003966,0.03,nc,nc73679151,2022-01-22T05:55:38.324Z,"4km NNW of The Geysers, CA",earthquake,0.31,0.8,,1,reviewed,nc,nc
2022-01-16T10:35:38.980Z,38.8068333,-122.7756667,0.31,1.66,md,42,33,0.007519,0.07,nc,nc73679146,2022-01-22T06:29:12.552Z,"4km NNW of The Geysers, CA",earthquake,0.14,0.24,0.232,16,reviewed,nc,nc
2022-01-16T10:31:57.900Z,42.5988333,-111.3646667,2.95,1.8,md,11,240,0.5727,0.06,uu,uu60477807,2022-01-18T16:34:12.700Z,"southern Idaho",earthquake,1.07,1.99,0.098,10,reviewed,uu,uu
2022-01-16T10:26:04.110Z,36.0208333,-117.8131667,1.59,0.77,ml,10,82,0.03842,0.07,ci,ci39913903,2022-01-18T18:06:30.125Z,"12km ESE of Coso Junction, CA",earthquake,0.15,0.21,0.086,3,reviewed,ci,ci
2022-01-16T10:17:06.670Z,40.7305,-112.0445,5.75,0.72,md,11,77,0.007449,0.12,uu,uu60477802,2022-01-18T16:03:21.110Z,"5 km ENE of Magna, Utah",earthquake,0.33,0.63,0.311,5,reviewed,uu,uu
2022-01-16T10:14:35.185Z,59.8897,-150.5866,46.1,1.5,ml,,,,0.4,ak,ak022qmmyox,2022-01-16T10:19:08.634Z,"21 km E of Fox River, Alaska",earthquake,,1,,,automatic,ak,ak
2022-01-16T10:01:22.940Z,38.8121681,-122.829834,1.97,0.85,md,10,122,0.003335,0.02,nc,nc73679141,2022-01-16T10:02:56.243Z,"8km WNW of The Geysers, CA",earthquake,0.37,0.7,,1,automatic,nc,nc
2022-01-16T09:48:51.626Z,61.4481,-148.5965,23.9,1.7,ml,,,,0.77,ak,ak022qm8up6,2022-01-16T10:17:28.204Z,"16 km E of Knik River, Alaska",earthquake,,0.2,,,automatic,ak,ak
2022-01-16T09:46:11.000Z,19.4086666666667,-155.2755,10.4,1.84,md,25,43,,0.16,hv,hv72876642,2022-01-18T21:23:30.490Z,"5 km SW of Volcano, Hawaii",earthquake,0.33,0.36,0.128911866710159,10,reviewed,hv,hv
2022-01-16T09:43:12.420Z,38.8163338,-122.8221664,2.72,0.87,md,22,51,0.009251,0.03,nc,nc73679136,2022-01-16T09:44:46.006Z,"7km NW of The Geysers, CA",earthquake,0.22,0.6,0.29,4,automatic,nc,nc
2022-01-16T09:30:18.920Z,37.6008333,-118.8075,7.12,0.22,md,9,264,0.02027,0.09,nc,nc73679131,2022-01-16T19:51:09.759Z,"12km WNW of Toms Place, CA",earthquake,1.65,1.02,0.258,8,reviewed,nc,nc
2022-01-16T09:26:26.303Z,59.6137,-152.1485,51.3,1.6,ml,,,,0.44,ak,ak022qm42zq,2022-01-16T09:30:02.670Z,"25 km SW of Anchor Point, Alaska",earthquake,,0.9,,,automatic,ak,ak
2022-01-16T09:24:00.180Z,37.4828333,-118.8506667,1.63,0.58,md,12,239,0.1084,0.03,nc,nc73679126,2022-01-16T19:41:38.656Z,"17km WSW of Toms Place, CA",earthquake,0.82,4.44,0.195,11,reviewed,nc,nc
2022-01-16T09:22:14.300Z,19.2275,-155.387333333333,30.68,2.8,ml,56,149,,0.13,hv,hv72876592,2022-01-19T03:00:41.684Z,"9 km ENE of Pāhala, Hawaii",earthquake,0.37,0.5,0.181189496465503,34,reviewed,hv,hv
2022-01-16T09:21:31.600Z,19.4068333333333,-155.272,12.47,1.14,md,25,52,,0.12,hv,hv72876587,2022-01-18T23:16:20.360Z,"5 km SW of Volcano, Hawaii",earthquake,0.42,0.3,0.146763119029287,8,reviewed,hv,hv
2022-01-16T09:19:19.960Z,17.916,-66.8555,16,2.78,md,24,192,0.0637,0.1,pr,pr2022016005,2022-01-17T03:06:02.974Z,"7 km SSE of Maria Antonia, Puerto Rico",earthquake,0.46,0.4,0.13,22,reviewed,pr,pr
2022-01-16T09:18:14.410Z,32.4055,-115.1826667,15.88,2.75,ml,29,126,0.1044,0.32,ci,ci39913895,2022-01-18T20:00:42.390Z,"6km N of Delta, B.C., MX",earthquake,0.48,0.85,0.207,16,reviewed,ci,ci
2022-01-16T09:16:57.260Z,19.1875,-155.502334594727,32.060001373291,2.00999999,md,33,88,,0.129999995,hv,hv72876577,2022-01-16T09:20:03.670Z,"3 km SW of Pāhala, Hawaii",earthquake,0.66,0.910000026,0.550000012,11,automatic,hv,hv
2022-01-16T09:16:52.334Z,61.3227,-147.5993,20.1,1.8,ml,,,,0.95,ak,ak022qm1zsy,2022-01-16T09:22:51.740Z,"54 km S of Glacier View, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-16T09:08:48.510Z,19.4236666666667,-155.278833333333,11.51,1.55,md,29,42,,0.16,hv,hv72876562,2022-01-19T00:25:49.570Z,"5 km WSW of Volcano, Hawaii",earthquake,0.39,0.27,0.12613488780297,11,reviewed,hv,hv
2022-01-16T09:07:45.510Z,38.8136667,-122.8168333,1.55,1.16,md,32,52,0.01077,0.03,nc,nc73679121,2022-01-21T23:08:13.462Z,"7km NW of The Geysers, CA",earthquake,0.17,0.25,0.15,5,reviewed,nc,nc
2022-01-16T09:07:36.287Z,38.1714,-117.8323,7.9,1.3,ml,11,114.56,0.105,0.1091,nn,nn00831787,2022-01-19T23:10:42.450Z,"34 km SE of Mina, Nevada",earthquake,,2.1,0.26,4,reviewed,nn,nn
2022-01-16T09:00:40.598Z,60.8998,-150.3588,44,2.4,ml,,,,0.53,ak,ak022qlyj0p,2022-01-16T19:57:10.567Z,"18 km E of Point Possession, Alaska",earthquake,,0.4,,,reviewed,ak,ak
2022-01-16T09:00:21.165Z,59.8643,-151.8608,181.3,2.4,ml,,,,1.04,ak,ak022qlyhhd,2022-01-16T09:04:38.960Z,"9 km N of Anchor Point, Alaska",earthquake,,1.7,,,automatic,ak,ak
2022-01-16T08:57:29.270Z,33.4895,-116.4461667,14.17,0.69,ml,31,108,0.03789,0.16,ci,ci39913887,2022-01-18T19:49:45.645Z,"22km ESE of Anza, CA",earthquake,0.26,0.41,0.169,16,reviewed,ci,ci
2022-01-16T08:53:59.080Z,35.9953333,-120.9861667,8.07,1.07,md,27,100,0.08391,0.1,nc,nc73679116,2022-01-21T23:40:04.649Z,"8km WSW of San Ardo, CA",earthquake,0.23,0.53,0.245,14,reviewed,nc,nc
2022-01-16T08:35:58.160Z,38.8334999,-122.8156662,1.39,0.85,md,7,91,0.011,0,nc,nc73679111,2022-01-16T08:37:37.561Z,"8km NW of The Geysers, CA",earthquake,0.43,1.47,,1,automatic,nc,nc
2022-01-16T08:33:22.180Z,19.408166885376,-155.275161743164,9.93000030517578,1.83000004,md,29,42,,0.159999996,hv,hv72876497,2022-01-16T08:36:30.490Z,"5 km SW of Volcano, Hawaii",earthquake,0.39,0.379999995,1.08000004,5,automatic,hv,hv
2022-01-16T08:32:42.350Z,14.5307,-60.543,34.14,3.9,ml,,161,0.402,0.71,us,us7000gcer,2022-01-18T23:32:51.915Z,"31 km E of Le Vauclin, Martinique",earthquake,5.5,4.6,0.073,25,reviewed,us,us
2022-01-16T08:22:21.310Z,33.9231667,-116.866,12.97,0.85,ml,37,76,0.106,0.12,ci,ci39913879,2022-01-18T19:43:57.106Z,"1km ESE of Banning, CA",earthquake,0.14,0.39,0.164,19,reviewed,ci,ci
2022-01-16T08:15:41.999Z,24.1908,122.2624,50.7,5.2,mww,,43,0.61,1.34,us,us7000gcej,2022-01-18T14:53:45.470Z,"70 km ENE of Hualien City, Taiwan",earthquake,4.2,2.6,0.086,13,reviewed,us,us
2022-01-16T08:07:15.011Z,51.8681,170.5695,10,4.1,mb,,209,2.332,0.4,us,us7000gcey,2022-01-16T09:09:23.040Z,"208 km WSW of Attu Station, Alaska",earthquake,13,2,0.066,62,reviewed,us,us
2022-01-16T07:58:55.050Z,33.2031667,-116.0165,7.15,1.55,ml,66,45,0.08091,0.22,ci,ci39913871,2022-01-18T19:36:17.380Z,"12km SSW of Salton City, CA",earthquake,0.15,0.57,0.197,23,reviewed,ci,ci
2022-01-16T07:49:19.490Z,38.8014984,-122.770668,1.22,0.85,md,9,94,0.008605,0.02,nc,nc73679096,2022-01-16T07:50:56.817Z,"3km NNW of The Geysers, CA",earthquake,0.47,0.77,,1,automatic,nc,nc
2022-01-16T07:41:00.290Z,19.4120006561279,-155.276992797852,11.5699996948242,1.76999998,md,22,52,,0.129999995,hv,hv72876397,2022-01-16T07:44:20.030Z,"5 km SW of Volcano, Hawaii",earthquake,0.57,0.289999992,2.00999999,4,automatic,hv,hv
2022-01-16T07:32:14.760Z,37.4905,-118.8633333,2.54,0.53,md,10,231,0.103,0.11,nc,nc73679091,2022-01-16T19:09:36.138Z,"18km WSW of Toms Place, CA",earthquake,0.91,3.05,0.159,9,reviewed,nc,nc
2022-01-16T07:32:03.660Z,33.598,-116.8053333,6.93,0.49,ml,17,80,0.04769,0.11,ci,ci39913863,2022-01-16T14:43:58.699Z,"13km WNW of Anza, CA",earthquake,0.25,0.47,0.16,11,reviewed,ci,ci
2022-01-16T07:30:21.050Z,38.7868333,-122.742,1.94,-0.08,md,15,84,0.005467,0.02,nc,nc73679086,2022-01-21T00:24:33.202Z,"2km NE of The Geysers, CA",earthquake,0.24,0.55,0.145,2,reviewed,nc,nc
2022-01-16T07:28:35.282Z,61.8126,-149.7216,19.1,1.5,ml,,,,0.78,ak,ak022qkxnwo,2022-01-16T07:41:49.844Z,"18 km ENE of Willow, Alaska",earthquake,,0.3,,,automatic,ak,ak
2022-01-16T07:24:51.950Z,44.3051667,-115.1586667,8.69,1.91,ml,9,82,0.917,0.25,mb,mb80536169,2022-01-16T16:05:48.530Z,"southern Idaho",earthquake,0.71,1.7,0.249,5,reviewed,mb,mb
2022-01-16T07:10:38.080Z,33.4818333,-116.4325,13.95,0.74,ml,21,41,0.04184,0.16,ci,ci39913855,2022-01-16T14:43:59.728Z,"23km SSW of La Quinta, CA",earthquake,0.31,0.61,0.113,19,reviewed,ci,ci
2022-01-16T06:53:43.950Z,19.2186660766602,-155.412338256836,31.8199996948242,2.13000011,md,45,142,,0.100000001,hv,hv72876302,2022-01-16T06:56:57.730Z,"7 km ENE of Pāhala, Hawaii",earthquake,0.58,0.74000001,0.409999996,20,automatic,hv,hv
2022-01-16T06:52:32.904Z,3.4987,96.5659,68.34,4.6,mb,,111,1.76,0.63,us,us7000gce3,2022-01-16T08:02:43.040Z,"86 km SE of Meulaboh, Indonesia",earthquake,3.7,7.3,0.071,58,reviewed,us,us
2022-01-16T06:52:14.540Z,35.6583333,-117.4948333,8.41,0.38,ml,9,158,0.07645,0.12,ci,ci37379492,2022-01-18T18:25:43.756Z,"15km SW of Searles Valley, CA",earthquake,0.75,0.54,0.174,2,reviewed,ci,ci
2022-01-16T06:51:54.090Z,37.4846667,-118.8436667,3.72,2.28,md,27,118,0.1058,0.05,nc,nc73679081,2022-01-16T20:10:11.077Z,"17km WSW of Toms Place, CA",earthquake,0.26,1.09,0.165,34,reviewed,nc,nc
2022-01-16T06:47:48.910Z,35.9228333,-117.7456667,11.22,0.6,ml,8,112,0.06418,0.05,ci,ci39913831,2022-01-16T14:44:26.021Z,"15km E of Little Lake, CA",earthquake,0.27,0.66,0.188,4,reviewed,ci,ci
2022-01-16T06:39:42.570Z,18.1576,-67.2528,18,2.68,md,13,182,0.1233,0.2,pr,pr2022016004,2022-01-16T07:00:49.635Z,"11 km NW of Puerto Real, Puerto Rico",earthquake,0.65,0.5,0.1,4,reviewed,pr,pr
2022-01-16T06:35:42.240Z,19.2240009307861,-155.400665283203,33.8899993896484,1.86000001,md,47,145,,0.119999997,hv,hv72876267,2022-01-16T06:38:53.830Z,"8 km ENE of Pāhala, Hawaii",earthquake,0.57,0.850000024,0.280000001,17,automatic,hv,hv
' > earthquakes.csv

echo '<!--
Copyright 2016 Google Inc.
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance wi
th the License. You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed
on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for t
he specific language governing permissions and limitations under the License.
-->

<html>
<title>Earthquakes this week</title>
<h2>Earthquakes this week</h2>
<img src="earthquakes.png" width="1000"/>
<p>
Download <a href="earthquakes.csv">original USGS data</a>.
</p>
</html>' > earthquakes.htm


touch earthquakes.png

export BUCK=$(cat /dev/urandom | tr -dc 'a-z0-9' | fold -w 63 | head -n 1)
gsutil mb gs://$BUCK
gsutil cp earthquakes.* gs://$BUCK/earthquakes/

```
