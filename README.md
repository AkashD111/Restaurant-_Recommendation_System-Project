# Restaurant-_Recommendation_System-Project
Project Name: Restaurant Recommendation System
Description: Building a restaurant recommendation system can be a fascinating and practical project. Such a system can help users discover new dining experiences based on their preferences. This Project is built using python programming language and Jupyter Notepad IDE is used for the development of this project.
Installation
Step 1. Find and open the Anaconda Prompt app using the search bar. Alternatively, you can use the Anaconda Powershell Prompt. The Anaconda Powershell Prompt has more bells and whistles and it is generally nicer to work with.
Step 2. Once the Anaconda Prompt (or Anaconda Powershell Prompt) app opens, navigate to the desired folder, using the cd command.
Step 3. Once in the desired folder, type jupyter notebook followed by the Enter key.
Step 4. The Jupyter server will start. You should see some server logs printed. You may be prompted to select an application to open Jupyter in. Firefox or Chrome are preferred.
Step 5. Create a new Jupyter notebook.
Step 6. Your new Jupyter notebook is now ready and you can start learning more about data types, variables, numbers, and more!  
Code Explanation:
# sample dataset considered for the Restaurant _Recommendation_System project, data is stored in the form of dictionary in key and value pair.
restaurant_data = {
    "Italian Delight": {'cuisines':["Italian","Indian","Mediterranean"],'ratings':5},
    "Spice Haven": {'cuisines':["Indian","Italian","Indian","Mediterranean"],'ratings':4},
    "Sushi House": {'cuisines':["Italian","Indian","Mediterranean","Japanese"],'ratings':4},
    "Mediterranean Bistro": {'cuisines':["Indian","Italian","Mediterranean","Japanese"],'ratings':2},
    "Taco Palace": {'cuisines':["Mexican","Italian","Indian","Mediterranean","Japanese"],'ratings':1},
    "Burger Joint": {'cuisines':["Mexican","Italian","Indian","Mediterranean","Japanese","American"],'ratings':4},
    "Dim Sum Paradise": {'cuisines':["Chinese", "Dim Sum","Indian","Mediterranean","Japanese","American"],'ratings':5},
    "French Fusion": {'cuisines':["French","American"],'ratings':4},
    "Greek Taverna": {'cuisines':["Greek", "Mediterranean"],'ratings':5},
    "Thai Spice": {'cuisines':["Thai", "Asian Fusion"],'ratings':4},
    # Add more restaurants with their cuisines
}

# cuisines_data function maps the restarants name and their cuisines
def cuisines_data():
    cuisines={}
    for i in restaurant_data:
        cuisines[i]=restaurant_data[i]['cuisines']
    return cuisines
# ratings_data function maps the restarants name and their ratings
def ratings_data():
    ratings={}
    for i in restaurant_data:
        ratings[i]=restaurant_data[i]['ratings']
    return ratings
# full_preference function it will return dictionary of all the restaurant name, cuisines based on highestrating
def full_preference(all_rating):# only sort of ratings
    import operator
    a=all_rating
    desorted=dict(sorted(a.items(), key=operator.itemgetter(1), reverse=True)) # to see the highest rating restaurnats
    return desorted
#print(full_preference(filter)) #this function call will select all the rating of cuisine
# top_three this function it will recommend top three cuisine for the user based on his input
def top_three(Full_preference):    
    top_three=list(Full_preference.keys())
    c=1
    print("Top Three Restarents are Recommended for you Inputed Cusines")
    for i in range(3):
        print(c,"'s preference is',top_three[i],'and its rating is:",ratings_data()[top_three[i]])
        c+=1

        
                    

# recommend_restaurants function that takes a user's input cuisines or food.
def recommend_restaurants(user_input):
    User_input=user_input.title() 
    def check_cuisine(User_input):
        l1=[]
        for i in cuisines_data():
            if User_input in cuisines_data()[i]: # to see input is present inside 
                l1+=[i]    #add all cuisines available restaurants in to l1
        return l1
    check_cuisine(User_input)
    Check_cuisine=check_cuisine(User_input)
    # result function it will check the cuisine and it will call the required functions and it will finally give the recommendation of cuisines to user
    def result(Check_cuisine):
        try:
            if len(Check_cuisine)==0:
                print("Sorry, we couldn't find any restaurants that serve", {User_input} ,"cuisine.")
            else:
                def Cuisine_rating(l1): #parameter l1 is list of restaurants available to serve cuisine as user inputed.
                    input_cuisine={}
                    for i in l1:
                        input_cuisine[i]=ratings_data()[i] 
                    return input_cuisine
                Cuisine_rating(Check_cuisine)
                AllCuisine_rating=Cuisine_rating(Check_cuisine) # ratings not as per ratings order
                Full_preference=full_preference(AllCuisine_rating) # Restauranst cuisines displayed as per ratings
                top_three(Full_preference)
        except IndexError:
                print('Only less than Three preference is available out of Top_Three Thank You')      
    result(Check_cuisine)
user_input=input('enter type of food')
recommend_restaurants(user_input)




