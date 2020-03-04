# flight-fare-alerts-automation

This repository contains set of files that has python code to perform an
 automated flight search using flights.google.com. It also has features to
    save the results to a spreadsheet, retrieve flight data and
   pricing information based on a given route and date or fetch the best
    price from the history of flight search results.
 
1.  Main program (<b>main_program.py</b>) that manages the user interface of the
 project (some of the options as sample below:)
 
        "Enter the option number you would like to try:\n\n"
            "1. Run the flight search and save results to the spreadsheet\n"
            "2. Perform a flight search with user driven parameters\n"
            "3. Exit "
            "-->  ")
            
            1. <enter>
                    
        Enter # of iterations and frequency in seconds separated by comma : 1
        ,3600
        
        Enter the option number you would like to try:\n\n"
                    
           "1. Search flight results by route and date \n"
           "2. Get the cheapest price by route \n"
           "--> "
           
           1. <enter>        
            
           "Enter the route and date in dddd-mm-yy format followed by comma "
                    "e.g: '1, 2020-02-06' \n"
                    "\t 1 -  MUC–BOS \n"
                    "\t 2 -  ZRH–BOS \n"
                    "\t 3 -  AMS–BOS \n"
                    "\t 4 -  ORY–BOS \n"
                    "\t 5 -  BCN–BOS \n"
                    "--> "    
                    2. <enter>
           
           "Enter the route for the cheapest price \n"
                    "\t 1 -  MUC–BOS \n"
                    "\t 2 -  ZRH–BOS \n"
                    "\t 3 -  AMS–BOS \n"
                    "\t 4 -  ORY–BOS \n"
                    "\t 5 -  BCN–BOS \n"
                    "--> "
                    4. <enter>
2.  <b>flights_search.py</b> which has code for iterating the
 flight search based on a set schedule and frequency and continuously scan
  the flight prices for the routes coded. 
  It also saves the results in a spreadsheet after each search. Multiple
   routes data is stored in separate worksheets within the same excel.
   Finally it also detects preferences on alerts if the price it finds has
    crossed the set amount and triggers an email notification.
    
        Uses the routes from the input dictionary and performs a google flights
        search. Invokes methods to save the results to excel.
        
        :param num_of_times: home many times to perform search
        :param frequency_in_sec: how much time between subsequent searches in
        seconds
        :param dict_of_routes: routes to perform searches on.
        :return: none
        
        SAMPLE RUN:
        
        1. Run the flight search and save results to the spreadsheet
        2. Perform a flight search with user driven parameters
        3. exit
        -->  1
        Enter # of iterations and frequency in seconds separated by comma :1,15
        city name:  munich
        city name:  zurich
        city name:  amsterdam
        city name:  paris
        Email sent : Flight Price drop for ORY–BOS To 334
        Email sent : Flight Price drop for ORY–BOS To 334
        city name:  barcelona
        Flight Records written to spreadsheet !

3.  <b>FlightRecord.py</b>, a class that represents a record returned by the search
 results from google flights.
 
          Flight record to represent a flight search object .
          Public attributes to store:
              1. airline_name
              2. price
              3. route
              4. stops
              5. duration
              6. timestamp
              7. departure_time
              8. arrival_time

          Methods :
              1. constructor
                  __init__ to initialize the objects
              2. display_header
                  displays the header names for the flight record object
              3. __repr__
                  formatted representation of the flight record response objects

            
4.  <b>SaveResults.py</b>,

    Class that saves the results from the automated flight search into a
    spreadsheet. Also has functionality to send email when invoked. Uses the
    gmail smtp server

        Attributes
            1. __xls_file
            2. __server
            3. __port

        Methods :
            1. constructor
                __init__ to initialize the objects
            2. get_xls_file
                returns the excel file used to save the flight search results
            3. save_xls
                method that saves the flight search results to the spreadsheet
            4. send_email_alert
                method that sends alert on a price drop using smtp library and
                connects to gmail server

5.  <b>SearchResults.py</b>

        Private attributes to store:
        1. __xls_file
        -  name of the excel file to use to retrieve the flight records
        2. __flight_records
        -  list of FlightRecord objects representing the results
        3. __lowest_price
        -  cheapest price for the route

        Private Methods  :
        1. flight_results(route, date_of_flight)
        -  return list of flight prices based on route and date range. It
           will return multiple results (list of FlightRecord ) if more than one
           flight records are present.
        2. best_price(route)
        -  searches the stored results in the spreadsheet and returns . if
           multiple best prices are available, the first record (
           FlightRecord) is returned
           
6.  <b>Flights_Tracked.xlsx</b>

       Sample data for one of the routes that is save to the spreadsheet is
        as below. There are multiple sheets within the excel with similar
         data that is relevant to that route

        	Timestamp	Departure - Arrival	airline_name	flight_duration	airport_codes	no_of_stops	flight_price
            0	1970-01-01 00:00:02	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $410    
            0	2020-02-02 15:32:59	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $410    
            0	2020-02-02 17:04:12	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $410    
            0	2020-02-02 17:21:19	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $410    
            0	2020-02-04 19:36:53	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $408    
            0	2020-02-05 21:54:26	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $406    
            0	2020-02-05 21:58:33	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $406    
            0	2020-02-05 22:58:58	   7:00 AM   –   1:20 PM   	 Tap Air Portugal    	 12h 20m   AMS–BOS   	 AMS–BOS 	 1 stop 	       $406    

7.  <b>Programming constructs used:</b>

        1. Panda dataframes, ExcelWriter class, read_excel method, series
        2. collections - dictionaries, lists
        3. While, for 
        4. if, elif, else
        5. try catch, except. command line input data validation
        6. smtp library
        7. classes, objects, public and private attributes, public and private methods
           , constructors and __repr__ for displaying objects as string representations 
        8. functions taking and returning values.
        9. MIME Multipart messages
        10. Selenium webdriver for chrome
        11. BeautifulSoup library to parse html. lxml HTML parser.
        12. divs and html scraping
        13. regular expressions to validate data. 
        14. string manipulation - split(), len() and strip(). Timestamp
         handling.
        15. search, sort lists and dictionaries.
        16. unit tests to assert methods in class SearchResults.py
        
