# Covid-19-Dashboard

## By Christina Rozario

Used the dataset from https://ourworldindata.org/covid-deaths


First I have downloaded the data from the website as Excel CSV file. After that I have imported dataset from Excel to Microsoft SQL Server. 
After cleaning the data and worked on the data I have copied data to Excel and uploaded to Tableau. 
Created data visualization regarding the Global Numbers and impact of Covid-19. 

### SQL queries used:

-- 1. Global Numbers

Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage
From PorfolioProject..['Covid deaths$']
--Where location like '%states%'
where continent is not null 
--Group By date
order by 1,2

-- 2. Total Death By Continent

Select location, SUM(cast(new_deaths as int)) as TotalDeathCount
From PorfolioProject..['Covid deaths$']
--Where location like '%states%'
Where continent is null 
and location not in ('World', 'European Union', 'International','High income', 'Upper middle income', 'lower middle income', 'Low income')
Group by location
order by TotalDeathCount desc

-- 3. Percent Population Infected Per Country

Select Location, Population, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected
From PorfolioProject..['Covid deaths$']
--Where location like '%states%'
Group by Location, Population
order by PercentPopulationInfected desc


-- 4. Percent Population Infected

Select Location, Population,date, MAX(total_cases) as HighestInfectionCount,  Max((total_cases/population))*100 as PercentPopulationInfected
From PorfolioProject..['Covid deaths$']
--Where location like '%states%'
Group by Location, Population, date
order by PercentPopulationInfected desc

### The link and the image of the dashboard given below:

![unnamed-chuck-2-3](https://github.com/ChristinaRo12/Covid-19-Dashboard/blob/main/Covid-19%20Dashboard.png)


Link to the Covid-19 Dashboard: https://public.tableau.com/app/profile/christina.rozario/viz/CovidDashboard_16642167917260/Covid-19Dashboard
