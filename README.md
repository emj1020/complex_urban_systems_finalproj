# complex_urban_systems_finalproj

This repo contains the final project for the Complex Urban Systems Spring 23 course at NYU CUSP.

### Research Question

Is there an association between the neighborhood commute time to job centers (calculated using the mode of public transit) with median income?  We hypothesize that increased commute times will correlate with decreased median income. 

If the correlation exists, we also want to investigate the relationship between race and commute time by controlling for income.


### Background

New York City provides an extensive public transit network with various modes of transportation such as subway, bus, commuter rail, and ferry services. However, the accessibility of public transit varies for New Yorkers. For instance, the city’s transit system has “historically been designed to serve and support areas with the greatest population density (NYC DOT, 2023).” Discriminatory policies such as redlining furthered this divide on transit accessibility. In early 2023, the New York City Department of Transportation (NYC DOT) made recommendations about priority areas for transit accessibility improvement investment according to their analysis of income, race, job availability, and commute time to illustrate the mobility pattern of New Yorkers. However, the details of their research methodology are not publicly available, nor did they use the highest granularity of data available. This project will examine the connection between job opportunities, demographic information, transit availability, and commute times using datasets with higher granularity and different modeling techniques. 

### Tentative Methodology

We plan to create two weighted networks of New York City: the number of commuters between neighborhoods and the public transit travel time between neighborhoods. 

The nodes of both networks will be the centroid of each census block group (CBG). CBG are a good approximation of a neighborhood with respect to size and there are demographic and commute data present at that spatial granularity. The edges of the commute network will be weighted by the number of people commuting between two neighborhoods. This weight may need to be normalized by the number of people who live in each neighborhood because the CBG population varies. The public transit travel time network consists of CBG centroids as nodes and edges weighted by the travel time between two neighborhoods based on the minimum public transit travel route. In theory, this travel time will be calculated using a network where the nodes will represent the subway and bus stops across the city, and the edge weight will be the travel time between the stops. Then the travel time between neighborhoods will be calculated using the Networkx Python library (dijkstra’s shortest path algorithm). However, we are still looking into the best way to determine public transit travel times across an entire network. We may only evaluate the travel time between neighborhoods and the identified job centers depending on the computational complexity of determining public transit commute time.

After both networks are built the first step is to identify a central business district (CBD) or job centers. We plan to look at the in-degree centrality of nodes to determine the neighborhoods to which people are commuting. Next we will calculate the commute time to the identified job centers. To calculate the average commute, we will use the travel time between all neighborhoods and the job centers provided by the public transit network and then either weight that by the percentage of people utilizing that job center or look at the commute time of the closest CBD to each respective neighborhood. Additionally, we will calculate the gini index both for commute times in a neighborhood and utilize the census bureau gini index for income to ensure that we are not overlooking neighborhoods with high inequality due to taking the average commute or income. 

### Data Selection 

* Work hotspots: Longitudinal Employer-Household Dynamics (LEHD) Origin-Destination Employment Statistics (LODES) from the Census Bureau will be used to map where people commute to work in order to identify hotspots of employment. 
 
* Public transit network: MTA General Transit Feed Specification (GTFS) feeds for the NYC subway and buses, along with the [Peartree](https://github.com/kuanb/peartree) python library, will be used to create a directed network of all public transit in New York City. We plan to use an estimate of travel time between the stops as an edge weight to measure connectivity to the identified hotspots of employment.

* Demographic data: American Community Survey data from the Census Bureau will be used to create neighborhood demographic profiles to compare neighborhood connectivity to various socioeconomic indicators.  

### Foreseeable Limitations 

* The LEHD-LODES data is only available through 2019; the impact of the pandemic on work and commuting trends will not be captured by our analysis. 

* Our network of public transportation will not incorporate multimodal trips such as biking or driving to the subway. 

* Travel time between stops will not incorporate wait times, planned service changes, or other delays. 

* Our neighborhood demographic profiles will represent the entire neighborhood, not just the subset of workers commuting to the job centers. 

* This analysis will focus exclusively on work commutes; a future analysis could replicate our design looking instead at social mobility outside of the work context. 

