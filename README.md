# bus_delay_prediction
Lab for testing multiple Machine Learning models using local traffic data to predict the average expected delay at a bus stop

**HEAVILY WORK IN PROGRESS**

## Raw dataset
The complete dataset is private.

But this is a little snippet of the used data. The data, which is used to train the models, has a range of 8 months and several million lines of data. 
| timestamp           | busStopID | stopName                    | patternText | direction    | actualTime | plannedTime | status     | routeId             | tripId              | vehicleId             |
|---------------------|-----------|------------------------------|--------------|--------------|------------|-------------|------------|----------------------|----------------------|------------------------|
| 2024-12-18 18:32:17 | 1020      | Heikendorf, Am Heidberg      | 15           | Mettenhof    | 18:52      | 18:52       | PREDICTED  | 1610073983892324384 | 1610077840787696906 | -7638104967705910578  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 13           | Kiel Hbf     | 18:33      | 18:33       | PREDICTED  | 1610073983892324382 | 1610077840787574030 | -7638104967705910932  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 11           | Wik Kanal    | 18:37      | 18:35       | PREDICTED  | 1610073983892324359 | 1610077840787451151 | -7638104967705910820  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 12           | Schilksee    | 18:37      | 18:36       | PREDICTED  | 1610073983892324353 | 1610077840787565838 | -7638104967705910672  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 11           | Dietrichsdorf| 18:39      | 18:38       | PREDICTED  | 1610073983892324359 | 1610077840787479822 | -7638104967705910884  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 11           | Wik Kanal    | 18:44      | 18:43       | PREDICTED  | 1610073983892324359 | 1610077840787467534 | -7638104967705910912  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 6            | Hassee       | 18:46      | 18:46       | PREDICTED  | 1610073983892324356 | 1610077840787827991 | -7638104967705910810  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 12           | Kiel Hbf     | 18:48      | 18:48       | PREDICTED  | 1610073983892324353 | 1610077840787569934 | -7638104967705910704  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 11           | Dietrichsdorf| 18:48      | 18:48       | PREDICTED  | 1610073983892324359 | 1610077840787455247 | -7638104967705910898  |
| 2024-12-18 18:32:17 | 1005      | Belvedere                    | 13           | Strande      | 18:51      | 18:51       | PREDICTED  | 1610073983892324382 | 1610077840788143370 | -7638104967705910868  |

## Todo / Notes
- [ ] Feature Engineering: regarding duplicated entries, hence the data was collected by a query every 15 mins
- [ ] Feature Engineering: more features like holiday yes/no, kieler woche yes/no, maybe even weather? Rush hour?

## Analysis of the used methods

### Linear Regression (Ridge)
WIP

### HistGradientBoostingRegressor
<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/85becfaf-ed69-4bac-96bd-dac026384869" />

MAE (Mean Absolute Error): 0.97 minutes 
RMSE(Root Mean Square Error): 1.94 minutes 
R^2 (R-squared Score): 0.0752 

Training R^2 Score: 0.2247 
Test R^2 Score: 0.0752

The big difference between the *Training R^2 Score* and *Test R^2 Score: 0.0752* suggests overfitting.

In general, the charts show that the model still underestimates delays.
We can try to improve this by Feature Engineering, hence we are already weighting delays longer than 5 minutes more heavily.
