# chartmaker - Download FAA digital raster charts and translate into mbtiles databases  

### Instructions:   
1.) This node.js application requires several other applications to be installed. See ***Debian*** example below.              
2.) Clone this repository - ***git clone https://github.com/N129BZ/chartmaker.git***            
3.) From a terminal prompt in the ChartMaker directory, enter ***npm install***                        
4.) Edit **settings.json** with a text editor and change the **ChartType** value to one of the types in the ChartTypes list                      
5.) Run the app via command **npm start**         
6.) Go do something else... depending on the desired charts, the process can take several hours to complete.
     
### Settings.json  
Since the FAA publishes charts 20 days *before* the official chart date, this application will automatically select                 
the appropriate chart date from the list of official FAA chart dates in the chartdates.json file.  Alternatively, you can pass              
a valid chart date argument when launching the application, in the format ***-d MM-dd-YYYY***.                     
                   
*  For example, the zoom range value can either be in the format **n-n**, or you can use a single zoom level **n**                
*  You can also change the **TiledImageQuality** setting to reduce mbtiles file size.   
*  To save disk space, you can set **CleanMergeFolder** to true.
   *  The merge folder can end up being as fat as 13 gigabytes for the entire chart set
   *  Quantized images are preserved in their own folder, these will be less than 1/3 the size of the merge folder
*  To preserve all of the processing folders, you can set **RenameWorkArea** to true.
   *  This setting will rename the **workarea** folder to include the processed chart date. 
                   
***(See details below in additional information for the all application settings.)***                                    

### Full Installation example on a Debian distro (your system may be different)
* Note that on some versions of Ubuntu, ```python-imaging``` has been replaced by ```python-pil```
```
# install required dependencies using apt as sudo, this assumes you already have Python installed
sudo apt install        \    
        git             \       
        perl            \
        imagemagick     \
        pngquant        \
        python-imaging  \
        gdal-bin        \
        nodejs          \
        npm             \
        unzip

# change directory to where you will clone chartmaker, for example:
cd /myinstalldirectory

# clone chartmaker
git clone https:github.com/N129BZ/chartmaker.git
                            
# change directory to chartmaker
cd /myinstalldirectory/chartmaker
                                   
# unzip clipshapes.zip 
unzip clishapes.zip
                                    
# install required node packages
npm install                                      
```
### Additional information       
The chart zip files are downloaded from the FAA digital raster chart repository and unzipped. The unzipping process will normalize the resultant GEOtiff images and their matching tfw world files to filenames with underscores in place of spaces.     
       
As of May 13,2023, the official chart release is for **04-20-2023. You can view those release dates in the chartdates.json file** or view the list at: https://aeronav.faa.gov/visual/10-07-2021/sectional-files. **Also note that the FAA publishes these chart files *20 days before* an official release date.**        
                       
                        
**settings.json:**                                                                                                              
```
{
    "ChartUrlTemplate": "https://aeronav.faa.gov/visual/<chartdate>/All_Files/<charttype>.zip",
    "TiledImageQuality": 75,
    "CleanMergeFolder": true,
    "RenameWorkArea": false,
    "ZoomRange": "5-11",
    "ChartType": "Terminal"
}
```
**charttypes.json:**
```
{
    "ChartTypes": [
        "Sectional",
        "Terminal",
        "Caribbean",
        "Helicopter",
        "Grand_Canyon_Air_Tour_Operators",
        "Grand_Canyon_General_Aviation"
    ]
}
```
### ToDo:    
Add IFR charts, etc.    
     
      
#### ***inspired by https://github.com/jlmcgraw/aviationCharts*** 

