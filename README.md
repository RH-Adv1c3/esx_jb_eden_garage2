# esx_jb_eden_garage
 Private garage system based on ESX


 **Requirements**:
 - esx_vehicleshop	or fxserver-esx_vehicleshop
 - ft_libs (https://github.com/FivemTools/ft_libs)

  **Features**:

 - Renaming cars
 - An exited vehicle can not be out again
 - Only owned vehicles can be inside
 - No vehicle duplication
 - Impound for police and mecano
 - Code optimisation with ft_libs
 - Fix glitch with cheat engine
 - ...



If you want to use Society Garages:
- First of all modify your vehicle shop that people can buy cars to their society (in owner column must be database name of the job)
- Then insert this to your script when on / off duty:
 ```
TriggerEvent("esx_eden_garage:EnableSocietyGarage", "police", true)

TriggerEvent("esx_eden_garage:EnableSocietyGarage", "police", false)
 ```
 
 
 ```SQL
 ALTER TABLE `owned_vehicles` ADD INDEX `vehsowned` (`owner`);
 ALTER TABLE `owned_vehicles` ADD `fourrieremecano` BOOLEAN NOT NULL DEFAULT FALSE;
 ALTER TABLE `owned_vehicles` ADD `vehiclename` varchar(50) NOT NULL DEFAULT 'voiture';
 ```


If you want the impound of police and mecano to work, paste those lines when you take your duty.

On-Duty:
```
exports.ft_libs:EnableArea("esx_eden_garage_area_police_mecanodeletepoint")
exports.ft_libs:EnableArea("esx_eden_garage_area_police_mecanospawnpoint")
exports.ft_libs:EnableArea("esx_eden_garage_area_Bennys_mecanodeletepoint")
exports.ft_libs:EnableArea("esx_eden_garage_area_Bennys_mecanospawnpoint")
```

Off-Duty:
```
exports.ft_libs:DisableArea("esx_eden_garage_area_police_mecanodeletepoint")
exports.ft_libs:DisableArea("esx_eden_garage_area_police_mecanospawnpoint")
exports.ft_libs:DisableArea("esx_eden_garage_area_Bennys_mecanodeletepoint")
exports.ft_libs:DisableArea("esx_eden_garage_area_Bennys_mecanospawnpoint")
```

#UPDATE

becasue people are not devs and they don't know how sql work ... insert these lines seperatly. look at what column you already have and which not, insert the colums you haven't:
```sql
ALTER TABLE owned_vehicle add plate varchar(50) NOT NULL;
ALTER TABLE `owned_vehicles` ADD INDEX `vehsowned` (`owner`);
ALTER TABLE `owned_vehicles` ADD `fourrieremecano` BOOLEAN NOT NULL DEFAULT FALSE;
ALTER TABLE `owned_vehicles` ADD `vehiclename` varchar(50) NOT NULL DEFAULT 'voiture';
```
And run this script once if you haven't plate column:
https://github.com/TanguyOrtegat/esx_jb_migrate

With Command migrate

#UPDATE 25/08
 ```sql
alter table owned_vehicles add vehicle_type varchar(10) not null default 'car'
alter table owned_vehicles add garage_name varchar(50) not null default 'Garage_Centre'
```
Pay attention that you will need to edit your airplane dealer and boatdealer to put it in that table owned_vehicles and in where clause in SQL: where vehicle_type='boat' (for example)

#UPDATE 10/12
Added options for translations and added sqls for english and french. DO NOT RUN ALL SQLS! Only choose the one that you want the language to be in. they are named owned_vehicles_en or fr for english or french.
