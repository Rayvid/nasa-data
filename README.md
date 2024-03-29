# Penguin savers team data strutures and sources

## Key data source - aerosols from AERONET https://aeronet.gsfc.nasa.gov/cgi-bin/print_web_data_v3

### For data import, non-typed structure used

    CREATE TABLE default.Aerosols (
      `AERONET_Site` String,
      `Date` String,
      `Time` String,
      `Day_of_Year` String,
      `Day_of_Year_Fraction` String,
      `AOD_1640nm` String,
      `AOD_1020nm` String,
      `AOD_870nm` String,
      `AOD_865nm` String,
      `AOD_779nm` String,
      `AOD_675nm` String,
      `AOD_667nm` String,
      `AOD_620nm` String,
      `AOD_560nm` String,
      `AOD_555nm` String,
      `AOD_551nm` String,
      `AOD_532nm` String,
      `AOD_531nm` String,
      `AOD_510nm` String,
      `AOD_500nm` String,
      `AOD_490nm` String,
      `AOD_443nm` String,
      `AOD_440nm` String,
      `AOD_412nm` String,
      `AOD_400nm` String,
      `AOD_380nm` String,
      `AOD_340nm` String,
      `Precipitable_Water` String,
      `AOD_681nm` String,
      `AOD_709nm` String,
      `AOD_Empty1` String,
      `AOD_Empty2` String,
      `AOD_Empty3` String,
      `AOD_Empty4` String,
      `AOD_Empty5` String,
      `Triplet_Variability_1640` String,
      `Triplet_Variability_1020` String,
      `Triplet_Variability_870` String,
      `Triplet_Variability_865` String,
      `Triplet_Variability_779` String,
      `Triplet_Variability_675` String,
      `Triplet_Variability_667` String,
      `Triplet_Variability_620` String,
      `Triplet_Variability_560` String,
      `Triplet_Variability_555` String,
      `Triplet_Variability_551` String,
      `Triplet_Variability_532` String,
      `Triplet_Variability_531` String,
      `Triplet_Variability_510` String,
      `Triplet_Variability_500` String,
      `Triplet_Variability_490` String,
      `Triplet_Variability_443` String,
      `Triplet_Variability_440` String,
      `Triplet_Variability_412` String,
      `Triplet_Variability_400` String,
      `Triplet_Variability_380` String,
      `Triplet_Variability_340` String,
      `Triplet_Variability_Precipitable_Water` String,
      `Triplet_Variability_681` String,
      `Triplet_Variability_709` String,
      `Triplet_Variability_AOD_Empty1` String,
      `Triplet_Variability_AOD_Empty2` String,
      `Triplet_Variability_AOD_Empty3` String,
      `Triplet_Variability_AOD_Empty4` String,
      `Triplet_Variability_AOD_Empty5` String,
      `c440t870_Angstrom_Exponent` String,
      `c380t500_Angstrom_Exponent` String,
      `c440t675_Angstrom_Exponent` String,
      `c500t870_Angstrom_Exponent` String,
      `c340t440_Angstrom_Exponent` String,
      `c440t675_Angstrom_Exponent_Polar` String,
      `Data_Quality_Level` String,
      `AERONET_Instrument_Number` String,
      `AERONET_Site_Name` String,
      `Site_Latitude` String,
      `Site_Longitude` String,
      `Site_Elevation` String,
      `Solar_Zenith_Angle` String,
      `Optical_Air_Mass` String,
      `Sensor_Temperature` String,
      `Ozone` String,
      `NO2` String,
      `Last_Date_Processed` String,
      `Number_of_Wavelengths` String,
      `Exact_Wavelengths_of_AOD_1640nm` String,
      `Exact_Wavelengths_of_AOD_1020nm` String,
      `Exact_Wavelengths_of_AOD_870nm` String,
      `Exact_Wavelengths_of_AOD_865nm` String,
      `Exact_Wavelengths_of_AOD_779nm` String,
      `Exact_Wavelengths_of_AOD_675nm` String,
      `Exact_Wavelengths_of_AOD_667nm` String,
      `Exact_Wavelengths_of_AOD_620nm` String,
      `Exact_Wavelengths_of_AOD_560nm` String,
      `Exact_Wavelengths_of_AOD_555nm` String,
      `Exact_Wavelengths_of_AOD_551nm` String,
      `Exact_Wavelengths_of_AOD_532nm` String,
      `Exact_Wavelengths_of_AOD_531nm` String,
      `Exact_Wavelengths_of_AOD_510nm` String,
      `Exact_Wavelengths_of_AOD_500nm` String,
      `Exact_Wavelengths_of_AOD_490nm` String,
      `Exact_Wavelengths_of_AOD_443nm` String,
      `Exact_Wavelengths_of_AOD_440nm` String,
      `Exact_Wavelengths_of_AOD_412nm` String,
      `Exact_Wavelengths_of_AOD_400nm` String,
      `Exact_Wavelengths_of_AOD_380nm` String,
      `Exact_Wavelengths_of_AOD_340nm` String,
      `Exact_Wavelengths_of_PW_935nm` String,
      `Exact_Wavelengths_of_AOD_681nm` String,
      `Exact_Wavelengths_of_AOD_709nm` String,
      `Exact_Wavelengths_of_AOD_Empty1` String,
      `Exact_Wavelengths_of_AOD_Empty2` String,
      `Exact_Wavelengths_of_AOD_Empty3` String,
      `Exact_Wavelengths_of_AOD_Empty4` String,
      `Exact_Wavelengths_of_AOD_Empty5` String
    ) ENGINE = Log

### Later, script used to extract required typed data

    CREATE TABLE Aerosols_bananasa ENGINE = Log AS
    SELECT 
        toDate(CONCAT(SUBSTRING(Date,7,4), REPLACE(SUBSTRING(Date,3,4),':','-'), SUBSTRING(Date,1,2))) as Date,
        toDecimal64(Site_Latitude, 10) AS Latitude,
        toDecimal64(Site_Longitude, 10) AS Longitude,
        MAX(toDecimal64(Ozone,10)) AS Ozone,
        MAX(toDecimal64(NO2,10)) AS NO2,
        MAX(toDecimal64(c440t870_Angstrom_Exponent ,10)) AS c440t870_Angstrom_Exponent,
        MIN(toDecimal64(Sensor_Temperature, 10)) AS Temperature,
        maxIf(if(toDecimal128(AOD_440nm,20) > -5 AND toDecimal128(AOD_440nm,20) < 0, toDecimal128(0,20), toDecimal128(AOD_440nm,20)),           if(toDecimal128(AOD_440nm,20) > -5 AND toDecimal128(AOD_440nm,20) < 0, toDecimal128(0,20), toDecimal128(AOD_440nm,20)) >= 0) AS AOD440,
        max(toDecimal128(Triplet_Variability_440,20)) AS Variability440,
        maxIf(if(toDecimal128(AOD_870nm,20) > -5 AND toDecimal128(AOD_870nm,20) < 0, toDecimal128(0,20), toDecimal128(AOD_870nm,20)),           if(toDecimal128(AOD_870nm,20) > -5 AND toDecimal128(AOD_870nm,20) < 0, toDecimal128(0,20), toDecimal128(AOD_870nm,20)) >= 0) AS AOD870,
        max(toDecimal128(Triplet_Variability_870,20)) AS Variability870
     FROM Aerosols
     GROUP BY Date, Site_Latitude, Site_Longitude
     
### And to get exactly same granularity as meteo data we create grid

    CREATE TABLE Aerosols_grid ENGINE = Log AS
    SELECT
        Date,
        (FLOOR(toFloat64(Latitude)*2)+0.5)/2 AS Latitude,
        (FLOOR(toFloat64(Longitude)*2)+0.5)/2 AS Longitude,
        Ozone,
        NO2,
        c440t870_Angstrom_Exponent,
        Temperature,
        AOD440,
        Variability440,
        AOD870,
        Variability870
    FROM
        default.Aerosols_bananasa

## Secondary datasource from "POWER Data Access Viewer" for temperature, humidity and wind speed provided as a grid

    CREATE TABLE Meteo (
        LAT String,
        LON String,
        YEAR String,
        DOY String,
        TEMP String,
        WIND String,
        PRECTOT String
    ) Engine=Log;
    
    --DROP TABLE Meteo_bananasa
    CREATE TABLE Meteo_bananasa ENGINE=Log AS
        SELECT
        toDecimal64(LAT, 10) LAT,
        toDecimal64(LON, 10) LON,
        addDays(toDate(CONCAT(YEAR, '-01-01 00:00:00')), toInt32OrZero(DOY) - 1) DATE,
        toDecimal64(TEMP, 10) TEMP,
        toDecimal64(WIND, 10) WIND,
        toDecimal64(PRECTOT, 10) PRECTOT
        FROM Meteo
