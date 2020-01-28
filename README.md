![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Change All Agent Job Owners With SQL
**Post Date: May 9, 2014**        #



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's a quick way to change all the Job owners in SQL Server Agent. Lets say you want to set all the owners to the SQL Server Agent Account called MyDomain\SQL_AGT.
You can do this across all jobs by running this simple TSQL Logic. Following the script you can find another set of logic that will check to see which Job owners were changed.</p>    


## SQL-Logic
```SQL
use msdb;
set nocount on
declare @new_job_owner varchar(50)
declare @change_job_owners varchar(max)
set @new_job_owner = 'TP\SQL_AGT' --sql agent service account. set @change_job_owners = ''
select @change_job_owners = @change_job_owners +
'use msdb; ' + char(10) + 'exec sp_update_job @job_name = ''' + name + ''',' + char(10) + '@owner_login_name = ''' + @new_job_owner + ''';' + char(10) + char(10)
from msdb..sysjobs where suser_name(owner_sid) not in ('MyDomain\SQL_AGT') -- change all owners that are not set to new job owner account. order by name asc
exec (@change_job_owners) --for xml path(''), type

```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

   
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

