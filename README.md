# concretecodingchallenge
Here's the place where all our code will go for the 23-24 year 2 coding challenge

filename = 'Concrete_Data_Yeh_final.csv'
variables = ['cement', 'slag', 'flyash', 'water', 'superplasticizer', 'coarseaggregate', 'fineaggregate', 'age', 'csMPa']

class PreProcessing:
    "The aim of this class is to successfully replace all the empty values from"
    "the file given, and to split the columns into their own series / arrays."
    def __init__(self, file):
        self.data = pd.read_csv(file)
        
    def FillNaN (self):
        # Here we used the .mean method to replace the NaN values from the original dataset. 
        # (Please check this as we may use an alternative fillna method)
        for i in self.data.columns:
            self.data[i].fillna(self.data[i].mean(), inplace = True)
        return self
    
    def SplitColumns (self, variablelist)-> dict:      
        # not sure what to do here, trying to split each column in the dataframe to their individual series / arrays. (To sort out)
        Dict = {}
        for variable in variablelist:
            Dict[variable] = self.data[variable].to_numpy()
        return Dict


test = PreProcessing(filename).FillNaN().SplitColumns(variables)
# Here, we will form global variables for each array. These can be recalled for scaling and modelling, however, it cannot visually show which variable its from unless specified in further code. 
for variable, array in test.items():
    globals()[variable] = array
