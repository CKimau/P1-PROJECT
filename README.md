# PHASE-1-PROJECT
    ##loading Aviation Data

    file_path = 'C:\\Users\\KimauC\\OneDrive - SAFAL GROUP\\Desktop\\DATA SCIENCE\\Phase 1 Project\\AviationData.csv'
    aviation_data = pd.read_csv(file_path, encoding='ISO-8859-1')



    #checking Info

aviation_data.info

    #checking NaN values

NaN_values = aviation_data.isnull().sum()
NaN_values

    #dropping Null values

cleaned_data = aviation_data.dropna()

cleaned_data.head().sum()

#checking new data after cleaning

cleaned_data.info()

# Standardizing the Injury.Severity column by replacing any entry that starts with "Fatal" to just "Fatal"

aviation_data['Injury.Severity'] = aviation_data['Injury.Severity'].apply(lambda x: "Fatal" if "Fatal" in str(x) else x)

aviation_data.head()


   #Saving Cleaned File
output_file_path = 'cleaned_aviation_data.csv'

# Saving the cleaned data to a CSV file without the index
cleaned_data.to_csv(output_file_path, index=False)

print(f"Cleaned data has been saved to {output_file_path}")


#Categorizing Data in New column Error.type to determine if the error is Pilot related or Mechanical 

df = pd.read_csv('cleaned_aviation_data.csv')

# Replacing 'Report.Status' with the actual name of the column if different
df['Error.type'] = df['Report.Status'].apply(lambda x: 'Pilot error' if 'pilot' in str(x).lower() else 'Mechanical error')

df.to_csv('updated_aviation_data.csv', index=False)


# Calculating  the survival rate and creating a new column 'Survival.Rate'
df['Survival.Rate'] = ((df['Total.Serious.Injuries'] + df['Total.Minor.Injuries'] + df['Total.Uninjured']) /
                       (df['Total.Fatal.Injuries'] + df['Total.Serious.Injuries'] + df['Total.Minor.Injuries'] + df['Total.Uninjured'])) * 100
df.to_csv('updated_aviation_data_with_survival_rate.csv', index=False)


# Loading the data from the uploaded file
file_path = 'C:\\Users\\KimauC\\OneDrive - SAFAL GROUP\\Desktop\\DATA SCIENCE\\Project P1\\final_updated_aviation_data_with_survival_rate.csv'
aviation_data = pd.read_csv(file_path)

# Standardizing the Injury.Severity column by replacing any entry that starts with "Fatal" to just "Fatal"
aviation_data['Injury.Severity'] = aviation_data['Injury.Severity'].apply(lambda x: "Fatal" if "Fatal" in str(x) else x)

# Creating a new column 'Fatality' which marks 'Fatal' for Fatal and 'Non-Fatal' for others
aviation_data['Fatality'] = aviation_data['Injury.Severity'].apply(lambda x: "Fatal" if x == "Fatal" else "Non_Fatal")

# Saving the cleaned DataFrame with the new 'Fatality' column to a new CSV file
aviation_data.to_csv('the_final_updated_aviation_data_with_fatality.csv', index=False)
