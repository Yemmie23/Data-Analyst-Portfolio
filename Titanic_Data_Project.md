
# The Titanic Disaster: A Data-Driven Exploration of Survival Factors

## Introduction
The sinking of the RMS Titanic on April 15, 1912, stands as one of the most infamous maritime tragedies in history. Known for its cutting-edge design and lavish features—including squash courts, a Turkish bath, a gymnasium, a barber shop, and the first-ever swimming pool on a ship—the Titanic set sail on its maiden voyage from Southampton, England, to New York City, USA. However, disaster struck when the ship collided with an iceberg in the North Atlantic, resulting in a swift sinking and the tragic loss of over 1,500 lives. Despite the high fatality rate, many passengers managed to survive, offering a compelling dataset to explore survival factors.

## Problem Statement
This analysis aims to uncover the key factors that influenced the survival chances of passengers aboard the Titanic. By examining variables such as age, gender, ticket class, and embarkation points, we seek to identify patterns that determined who survived and who didn’t.

Microsoft Excel was the primary tool used for conducting this analysis.

## The Dataset
This Titanic dataset comprises data on 891 passengers who were aboard the Titanic during its tragic maiden voyage. The dataset covers passengers only, not crew. The dataset for this study was obtained from Kaggle.

### Features
- **Passenger id**: Uniquely identifies passengers
- **Survival**: Survival (0 = No; 1 = Yes)
- **Pclass**: Passenger Class (1 = First Class, 2 = Second Class, 3 = Third Class)
- **Name**: Name of passengers (Full name)
- **Sex**: Gender (Male or Female)
- **Age**: Age of passenger
- **SibSp**: Number of siblings/spouses aboard
- **Parch**: Number of parents/children aboard
- **Ticket**: Ticket number
- **Fare**: Passenger fare
- **Cabin**: Cabin number
- **Embarked**: Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)

## Data Cleaning
The dataset was first imported into Microsoft Excel before beginning the cleaning process.

### Pclass
The 'pclass' column originally used numerical values (1, 2, and 3) to represent passenger classes. To make the data more understandable, I converted these numbers into their respective class names: 'First Class', 'Second Class', and 'Third Class’. The column was also renamed to 'Passenger Class'.

### Survived
The ‘Survived’ column was cleaned similarly, replacing 1 with 'Survived' and 0 with 'Dead'. Additionally, the column was renamed to ‘Survival Status’.

### Name
The ‘Name’ column was split into multiple columns using the "Split-to-Column" function in Excel. Titles, first names, and last names were combined into a single 'Full Name' column using the CONCAT function.

### Sex
The ‘Sex’ column contained the gender of each passenger. It was cleaned by changing the records to Proper Case using Excel’s Proper Function. The column was renamed ‘Gender’.

### Age
The ‘Age’ column had missing values, which were filled using the median age of the passengers. Additionally, a new column called ‘Age Group’ was created to categorize passengers.

### Parch and SibSp
The 'Parch' and 'SibSp' columns were summed to create a new column called ‘Family Size’.

### Ticket and Cabin
The 'Ticket' and 'Cabin' columns were not required for analysis and were deleted.

### Fare
The 'Fare' column was formatted as Currency ($) and rounded to 2 decimal places.

### Embarked
The abbreviations in the 'Embarked' column were replaced with the full port names: Southampton, Cherbourg, and Queenstown.

## Analysis and Visualization
Of the 891 passengers aboard the Titanic, only 38.3% (342) survived, while a tragic 62.6% (549) lost their lives.

### Gender Analysis
Although women made up only about 35.2% of the total passengers, their survival rate was much higher compared to men. Notably, 26.2% of female passengers survived while just 12.2% of male passengers did. The "women and children first" policy significantly increased their chances of survival.

### Passenger Class Analysis
Third-class passengers made up the majority at 55.2%. Among first-class passengers, approximately 15.3% survived, second-class passengers had a survival rate of 9.8%, while third-class passengers had the highest fatality rate with only 13.4% surviving.

### Embarkation Port Analysis
Of the passengers who boarded in Cherbourg, 10.4% survived. Queenstown had a lower survival rate with just 3.4% surviving, and Southampton had the highest fatality rate.

### Age Category Analysis
Young adults (ages 19–30) experienced the highest fatality rate despite their substantial representation. Children (≤18 years) and older adults (>50 years) had relatively lower survival rates.

## Recommendations
- **Strengthen Safety Measures and Regulations**: Enhance maritime safety protocols to prevent future tragedies.
- **Ensure Equitable Access to Safety Resources**: Distribute life-saving resources fairly among all passengers.
- **Implement Comprehensive Training Programs**: Provide thorough training on emergency procedures.
- **Increase Public Awareness**: Raise awareness about maritime safety and disaster preparedness.

## Conclusion
In summary, this analysis of Titanic data has provided insights into the factors that influenced survival during the ship's sinking. By leveraging data to inform safety protocols and increasing awareness about emergency preparedness, we can work towards preventing future tragedies like the Titanic disaster.
