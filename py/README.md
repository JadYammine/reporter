# Downloading Tiles

We have created a script that gives you the ability to fetch a subset of Valhalla tiles from S3.  The script uses a bounding box to determine the list of tiles that intersect with the bounding box.

Or, you can always view the [listing of tiles](https://s3.amazonaws.com/reporter-tiles/listing.html) to see if any updates have been pushed up to S3.

### Prerequisites

1. You must have Python 2.x installed on your computer.
2. You must also have cURL installed on your computer. (Usually available on every Linux, Unix, and Mac machine.)
3. To download a copy of the scripts, you can either:
    - Use Git to clone a copy of this repository for local use: `https://github.com/opentraffic/reporter.git`
    - Download a ZIP archive of the repository: `wget https://github.com/opentraffic/reporter/archive/dev.zip`

### Run via the command line

```sh
./download_tiles.sh `Bounding_Box` `URL` `Output_Directory` `Number_of_Processes` `Tar_Output`
```

`Bounding_Box`: This is the bounding box that will be used to fetch the subset of tiles.  The format is lower left lng/lat and upper right lng/lat or min_x, min_y, max_x, max_y (e.g., NYC Bounding box: `-74.251961,40.512764,-73.755405,40.903125`)

`URL`:  This is the prefix of the URL where the tiles are located.  For example, if the full URL for a tile is https://s3.amazonaws.com/reporter-tiles/planet_2017_06_16-14_39_57/2/000/753/542.gph, you would enter `https://s3.amazonaws.com/reporter-tiles/planet_2017_06_16-14_39_57`.

`Output_Directory`:  This is where the tiles will be created.  NOTE: Output directory will be deleted and recreated.

`Number_of_Processes`:  This is the number of cURL requests that you want to run in parallel.

`Tar_Output`: {True|False}: do you want the tiles tar'd up after they are download? This is an optional parameter that defaults to False.

***Example Usage***:

```sh
./download_tiles.sh -74.251961,40.512764,-73.755405,40.903125 https://s3.amazonaws.com/reporter-tiles/planet_2017_06_16-14_39_57 /data/tiles 5 false
```

***Possible Failures***:

If cURL reports and error the script will report on what tiles were not downloaded.  This could be due to issues from connection problems, to a high number of processes being set, or just the fact that tile no longer exists.  For example:

```
[WARN] https://s3.amazonaws.com/reporter-tiles/planet_2017_06_16-14_39_57/2/000/753/542.gph was not found!
```

A listing of the tile files is saved to files.txt.  Moreover, cURL output is saved to curl_output.txt.
