# RobustaTask

### Note1: Everything is related to the below numbers in the code depending on the written statements sequence not regarding the execustion
### Note2: Project id documented on the second branch, You can check the demo below...

 ## First Commit 
 1. Creating the APIService class + Model:
 
   - In this commit I have used the native way in swift to retrieve the data from the API by using the **URLSession** and **Codable** 
   
    1.1 Simply created a shared instance to be able use the class functionality through it
   
    1.2 Created function and I returned the the response and the error in the completion , Make it escaping as I need it to be called after the function it was passed to returns
   
    1.3 Creating the API related vars/Constants like the url, urlSession, task
   
    1.4 Chcecking if there is an error, then checking if there is data existed
   
    1.5 Using try catch block to decode the response and completion on it or on an error if existed
   
    1.6 Once the task is created it supposed to be in suspended state so that's why we are using .resume to start the task
    
   2. Repo.swift

     2.1 Create owner struct with preperty for the owner name and adapt from Codable.
     
     2.2 Creat the main struct for the response which is called Repo and add the requested properies inside it ( Note: Can't find the date in the data passed )
  
  ## Second Commit
  3. Create the design for the tableView and it's functionalities
    
    3.1 Create a new nib file called **ReposViewController** to have a tableView and searchBar
    
    3.2 Take the outlets for these designs
    
    3.3 Set the tableViewDelegate and DataSource

    3.4 Call the functions of the tabkeView Delegate and DataSource

    3.5 Create a dummy xib cell to be used in the future

    3.6 In AppDelegate set the **ReposViewController** as the rootViewController
    
    3.7 Remove the Main.storyBoard file and remove it from the app general settings and from info.Plist as well

 ## Third Commit
  4. Create Protocol to conect the presenter and ViewController together
    
    4.1 Protocol : GetReposProtocol
    
    4.2 This protocol holds one function for now to retrive the data of repos -> presentRepos
    
   5. Create RepoPresenter
   
    5.1 Create typealias called **RepoPresenter** to be combination between viewController & my protocol to be able to use it in the future on my viewController.

    5.2 Create a weak var delegate from this typealias to be used
    
    5.3 Create a function to get the repos from my service
    
    5.4 Call the APIService function and present the data
    
    5.5 Call the delegate function to present repos
    
    5.6 Set the delegate 
    
   6. Back to **ReposViewController** :
  
    6.1 Create a lazy var from the presenter ( Lazy as I don't need to use it untill It's called )
    6.2 Just conform to the protocol and set my array + Reloading the tableView
    6.3 Set the delegate
    6.4 call the getRepo function from the presenter
    
   7. Go to **RepoCell** :
  
    7.1 Add the labels and the imageView
    7.2 Set the outlets
    
  ## Fourth Commit  
  
   8. Go to **Extenions** :
  
    8.1 Create UIImage Extension and create a function takes string as a parameter
    8.2 Make sure that url is existed
    8.3 Use GlobalQueue to make sure that images are being downloaded in the background + Weak self to avoid memory leak
    8.4 check on data and image
    8.5 assign the image + Using main queue to avoid errors due to undifiend or unexpected behavior that it may try to access the image but can't find it.
    8.6 I have faced an issue so the images weren't being set correctly so I have saved them using NSCache
    8.7 getting the image from the cache using its own key which is the url
    8.8 Saving the image into the cache
    8.9 Set the imageView outlet in **RepoCell**
    8.10 using the extension in **ReposViewController** datasource
    
   9. Create viewcontroller for RepoDetails :
  
    9.1 Create repo var to the value into
    9.2 Create viewController Design using scroll and stack views and setting outlets
    9.3 Moving to the delegate in **ReposViewController** and create the didselect function and pass the instance at each time
    9.4 Set the data using the passed instance and called it in the viewDidLoad
  
  ## Fifth Commit  
  
   10. SearchBar 
   
    10.1 Apply the delegate on the search bar outlet (change func to be setTableViewAndSearchBar)
    10.2 Create an array for searchedItems & Active status 
    10.3 Use the delegate function DidChange to check on text at each time changes
    10.4 Filtering the array with the searched text and return the range related to this filter
    10.5 Check if there is a searchedText or not to be able to retrive the data and reload tableView in all cases
    10.6 Changing in the data source at each time to check if search is active or not and depending on the status I will choose to return searched data or the normal one
    
   ## Sixth Commit
   
   11.Pagination
    
    11.1 In **ReposViewController** created two variables related to pagination and reposPaginationArray to hold 10 elements increased by 10 at each scroll
    11.2 Assigned the limit to the main repoArray count, and set the first 10 elements in reposPaginationArray
    11.3 Create function to check at each time number of available pages 
    11.4 Check if numberOfPages has passed the limit so will return and end the func
    11.5 Check if numberOfPages greater than or equal the limit - 10 -> (Last 10 elements will be added)
    11.6 The normal case to add elements 
    11.7 Reloading the tableView in all cases
    11.8 Adding **scrollViewDidEndDragging** to use the created function in it and at each time I'm comparing the y posistion + height with all the content size to decide if I can scroll or not

# Demo

![GIF](https://user-images.githubusercontent.com/26345314/146549716-f1349cbc-496e-471b-9108-54d2234e2402.gif)
