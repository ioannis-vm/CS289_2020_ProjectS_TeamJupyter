# CS289 Group Project S - Early Deadline Deliverables

### Group Member Info

| Name       | SID |
| ----------- | ----------- |
| Jaewon Lee | 3035373160 |
| Ioannis Vouvakis Manousakis | 3035352698 |

## What this is about

This repository contains instructions and code that can interact with Stellarium and retrieve data from the software in an automated fashion. It includes two jupyter notebooks.

| Notebook | Function |
| ----------- | ----------- |
| Stellarium_API.ipynb | Used to retrieve the data |
| dfGathering | Used to combine the retrieved data |


#### Stellarium?
Stellarium is an open-source free-software planetarium, licensed under the GNU General Public License version 2, available for Linux, Windows, and macOS. A port Stellarium called Stellarium Mobile is available for Android, iOS, and Symbian as a paid version developed by Noctua Software. All versions use OpenGL to render a realistic projection of the night sky in real-time.
[Source: wikipedia](https://en.wikipedia.org/wiki/Stellarium_(software))

## About versions
The development of these notebooks was performed using Python version 3.7.6 and  Stellarium version 0.20.3. The code was tested on Windows 10, Ubuntu 20.04, and Mac OS version Catalina 10.15.7.
Our code requires installing the following packages. We also list the version of those packages that was installed on our system during the development of the code.

- beautifulsoup4 (4.8.2)
- numpy (1.18.1)
- jdcal (1.4.1)
- pandas (1.0.1)
- tqdm (4.42.1)


## How to set things up
Using the jupyter notebooks provided herein requires having Python 3 and Stellarium installed. 

[Get Stellarium here](http://stellarium.org/)

There are a couple of necessary steps that one needs to take before using the provided jupyter notebooks.

1. **Enable the remote control plugin**. Open Stellarium and press F11 on the keyboard to get out of full-screen mode. Then, press F2 to bring up the Configuration menu. On the top pane, click the Plugins tab. On the left, navigate to Remote Control. Check the *Load at startup* checkbox. Then close the window and restart Stellarium. Press F11, then F2, navigate back to the Remote Control page and click configure. You need to check the two boxes on top that read "Server enabled" and "Enable automatically on startup" Make sure the port number reads **8090**. If you would like to use a different port, you will have to manually update that number in the notebooks. We haven't tried changing the port. Click Save settings and close the window. Restart Stellarium. *Note that you will only have to do this once.*
2. **Time zone - location settings**. Press F6 to bring up the Location window. You will need to uncheck the box that reads *"Get location from Network"*, check *"Use custom time zone"* and uncheck *"enable daylight saving time"*. Set the Country field to *"___"*, and the Time zone to *"UTC+00:00"*. Set the Longitude and Latitude information to zero. *You will need to do this, otherwise sometimes the location does not update*. Minimize the window. That's it! *Note that we have not found a command that can do those things using the API. You will have to change those settings each time you start Stellarium to use the jupyter notebooks provided herein*.



## Overview of the notebooks

### Stellarium_API.ipynb
This jupyter notebook contains a series of functions that enable the interaction with the Stellarium remote control plugin via HTTP requests. Specifically, it allows for changing the current time and location and retrieving a subset of the information that Stellarium outputs for a given celestial body. This functionality can be combined in various creative ways to create datasets of *synthetic observations*. It contains a full usage example, but the users are welcome to experiment or alter the code as needed for their particular use case scenario (i.e., retrieving different kinds of information than what we have implemented or have a different list of bodies of interest).

##### A note on speed
In our machines, we were managing to get up to 90 observations per second. For best results, it is advisable to start with a clean launch of Stellarium, change the necessary initialization parameters described in step 2, and keep the window minimized while python is doing its thing. We have not tried to parallelize the code. Still, we assume that it could result in bugs since we only have one instance of Stellarium running, and sending requests in parallel would result in getting back observation results that do not match what we assume they match. However, if acquiring large amounts of data is your goal, and you have the resources, you can always manually distribute the load to multiple machines and combine the resulting dataframes using the second notebook we provide.

### dfGathering.ipynb
In the case where many datasets are created using the previous notebook (perhaps by distributing the data gathering on many machines to speed it up), this jupyter notebook contains code to merge the dataframes.

## Our usage example
As a usage example, we have gathered synthetic observations of the locations of the planets of the solar system, the Sun and the Moon, as seen from an observer in Athens, Greece, for a period starting from -1500 BC and ending in 2020, taking at least one daily sample for each body of interest. Specifically, the celestial bodies for which we have collected data are the following:

- Mercury
- Venus
- Mars
- Jupiter
- Saturn
- Uranus
- Neptune
- Moon
- Sun

The data that we gathered were the following:

- Right Ascension (RA) (on date)
- Declination (Dec) (on date)
- Azimuth (apparent)
- Altitude (apparent)
- Distance
- Distance from the Sun
- IAU Constellation

The dataset can be used to apply a great variety of machine learning techniques, ranging from simple regression to nonlinear model fitting and neural networks, to manage to predict the observed parameters at any given universal time.

Our final dataset is stored in the form of a pandas dataframe in binary form (using pickle), and it takes up XXX Gb. Converting it to text to store it as a CSV would drastically (and unnecessarily) increase its size. It is too large to be hosted on GitHub, but it is available for public use and can be accessed  [here]().
It can be loaded back on memory with the following python line:

```
pickle.load(open('Historic_Observations.df', 'rb'))
```

> Happy astronomical exploration, and keep looking up!

*Feel free to contact us via email if you have any questions or concerns.*


