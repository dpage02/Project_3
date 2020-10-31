# Project_3

# Background 
In 1984, Boston College's Doug Flutie threw a game winning Hail Mary against powerhouse Miami to put a wild end to an underdog story. This last- second desperation attempt is thought to be one of the greatest unintentional marketing moments of all time.

In a study done by Harvard Business School Assistant Professor of marketing Doug J. Chung, it was found that on field success contributed to an 18.7% rise in applications and allowed schools to be more academically sellective. He mentioned that in order for schools to match these results they would need to either lower tuition by 3.8% or increase education quality through higher-quality faculty.


## Data 
Admissions data was taking from National Center for Eductional Statistcs (https://nces.ed.gov/ipeds/use-the-data). Athletic Expense data was taken from College Athletics Financial Information (CAFI) Database. 

##Tableau Visualization Writeup
Using tableau for this project, the goal  was to analyze the data and create visualizations that shows correlation between championship and admissions for universities football program over the past two decades. The foundation for our project is based on the Doug Flutie Effect concept that says if a school wins a championship, that school would yield higher enrollment.  The process used for the visualizations is outlined below: 
·      Utilized Python to perform ETL on our raw datasets to generate multiple cleaned csv datasets
·      Imported cleaned datasets into Tableau
·      Performed inner join on the School name from the Champion dataset and Admission dataset 
·      Created Champion vs Number of Applicants to analyze number of applications as it relates to the year the school won the championship. 
·      Created Applicants vs Number Admitted to assess correlation between these data points. 
·      Created interactive dashboard comprised of the two visualization.  The dashboard allow users to filter by school.
·      The dashboard was published via Tableau Public portal. 
·      Embed script for the dashboard from the Tableau Public Portal into our HTML code, for our hosted site.

## ML Findings and write up 

## Initial Data Cleanup and Exploration
We initially wanted to build a model that utilized multiple independent variables to predict potential revenue. Our first idea (that didn't prove to be a viable option) involved creating a forecasting model for all Power 5 conference football programs. Our goal was to deliver a calculator that could predict where a program would be in 5 years given different expenditures and cash inflows related to the football team, as well as how these revenues/outflows affected application amounts to each college. Our hypothesis was that the more a school invests in its football team over time, the team would perform better thus resulting in more college applications. We began by cleaning up the data which involved finding and replacing any '$0' values with '$1' to avoid the 'divide by zero' error when creating the correlation matrix. Changing these values is statistically insignificant since the dollar amounts attributed to the other variables range from the tens of thousands to hundreds of millions. We also got rid of any rows containing  'NaN' values since the dataset contained over 3,000 rows, dropping a few columns didn't affect the overall datset. The next step was to merge the college application dataset with all of the Power 5 conference schools. Our data was limited due to only 35 out of approximately 70 Power 5 schools reporting their historical college application numbers. The dataset was further limited to the schools that also reported their in-depth historical football expenditures and revenues. This option proved to be unviable because there are too many factors that influence college applications. Sure, some schools will recieve more applications because their football team is good, but other factors like academics, tuition costs, and SAT and ACT scores influence where an applicant will apply. This inital data cleaning and exploration is reflected in the "John_Cleaning.ipynb" and "Expenses_MultiRegress_Model.ipynb".

## Second Try
Since our initial idea was not a viable option, we decided to pivot into predicting revenues based on 6 different historical cash outflows and inflows. We created a correlation matrix to figure out which independent variables were most correlated with "total revenues" to use in our model. We then created simple linear regression scatter plots to prove linearity between our independent variables and revenue. We then created a multivariate regression model using 'Coaches Compensation', 'Facilities and Equipment Expenses', 'Recruiting Expenses' as cash outflows, and 'Advertising Revenues', 'Donations', and 'Ticket Sales' to represent cash inflows. The model was accurate, but it was borderline impossible to visualize the data in a meanigful way. We tried plotting a of least squares 3D plot using MPL Toolkits and Statsmodels as seen near the end of the 'Expenses_MultiRegress_Model' notebook. Looking back, we should have used a time series ARIMA model to forecast predicted revenue with our 6 cash inflow and outflow variables to find the 'magic numbers' that schools could use to plan their football spending and revenues in order to have a profitable program. 

## Viable (sort of) Model
Since we didn't use a time series model (due to time contraints), our goal shifted from forecasting to predicting potential profit based on 'Total Expenses' in order to create a simple plot that could be used by football programs of all sizes to plan out their total football program budget in order to make their program profitible. We ran our model using 'Total Revenues' as the dependent variable, and 'Total Expenses' as the independent variable. We used the test variables to find 'Predicted Expenses' and 'Predicted Revenues'. We then subtracted 'Actual Expenses' from 'Predicted Revenues' to find 'Predicted Profit'. We then plotted a simple univariate regression plot with 'Predicted Profit' on the y-axis and 'Actual Expenses' on the x-axis as seen in the plot in 'Expenses_MultiRegress_Model' notebook. 

## Findings and Considerations
The r2 value is negative, telling us that the model is inaccurate at precicting potential profit based on expenses alone. As we can see in the 'Actual' points on the plot, the dataset is very large and encompasses many different levels of programs. The profitibility of the program does not necessarily reflect the total expenditures. Spending a lot of money does not always translate into profitibility. The data is evenly distributed along all expenditure amounts and profit (or lack there of) amounts. Our linear regression line shows how much a school SHOULD make depending on their total expenses, but there are just too many factors influencing whether or not a school is profitible. If a football program is spending X amount and they fall short of predicted profit Y, they need to evaluate the other factors that are highly correlated with revenue (the ones we looked at in the second model attempt) and make the appropriate capital investments in the program, or focus on increasing their various revenue streams. Looking at the regression plot, we can see that our model is better at predicting the profitability of smaller schools. As schools spend more, their predicted profitability becomes more widely distributed about the regression line. We attribute this phenomenon to larger schools having more revenue streams outside of football, such as endowments, more money from tuition and higher donation amounts due to a larger alumni base. Larger schools are able to absorb the higher expenditure and higher deadweight loss attributed to their football programs because they simply have more money to lose compared to smaller schools with smaller budgets. If we had more time (and better ML expertise) we would have liked to include or eliminate more independent variables that could predict a football program's profitibility. We also would have liked to find the 'magic numbers' for all of the independent variables mentioned before to give teams an idea of how much they need to spend and make in various areas. If we had more time we wanted to incorperate our findings into a calculator so any school could input their maximum expenditures as afforded by their budget to figure out their predicted profit and predicted cash flows. This was our first attempt at creating a predictive model, so we are proud of our work and feel that this is a good point to springboard into further learning and exploration. 
