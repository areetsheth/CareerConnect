# Stage 4 Final Report

## Please list out changes in the directions of your project if the final project is different from your original proposal (based on your stage 1 proposal submission).

We initially planned for the user to select many parameters of their ideal job, which would then keyword search based on these parameters - much like LinkedIn with an extra step at the end. Then, given the selected jobs/companies, the webapp would recommend N classes to the user. We would also save these searches in a separate database. 

We changed the direction of the project because we realized students would most likely use this as a quick resource when they wanted to choose classes and make a career/course plan. However, students could also benefit from the stored searches, so that is something we could add in the future. However, we offer many different query and search options for the user to obtain the information they desire. 

## Discuss what you think your application achieved or failed to achieve regarding its usefulness.

We believe our application is highly useful given its main user base. Students can load the application and receive information on which classes are the most useful given their job and career goals. This also allows them to see different job postings, career paths, and, company ratings. It also allows them to add their own courses, jobs, or companies. Imagine you are a young undergraduate student, without internships and experience. This website can easily propel you on the right path, by allowing you to think about your career goals and helping choose the perfect classes. We all wish this resource existed and CareerConnect definitely solves the need. 

However, there are many limitations. The web app is slightly confusing to use, some job postings and companies are not fully updated, and the recommendation engine is not perfect. However, these attributes can all be improved. The overall goal of usefulness was achieved.

## Discuss if you changed the schema or source of the data for your application.

As we discussed in [stage 2](https://github.com/cs411-alawini/sp24-cs411-team103-TopDB/blob/main/doc/Stage2_DatabaseDesign.md), the dataset that we chose to use, while very large for our needs, was not very clean and organized. We encountered multiple entries on one table that implied another in a different table did not exist (for example, a job description that used a company id, but there were no companies with that company id), and we had to check and fix all these inconsistencies before ingesting that into our DB, as that alone would violate many of our foreign key constraints. Once we managed to process the original dataset into our schema, however, we did not need to change any of the design choices following stage 2. For more details on how exactly we processed the original dataset into our DB with the proposed schema, please refer to the [stage 2](https://github.com/cs411-alawini/sp24-cs411-team103-TopDB/blob/main/doc/Stage2_DatabaseDesign.md) docs and the [processing/ingestion code](https://github.com/cs411-alawini/sp24-cs411-team103-TopDB/blob/main/data/data_ingestion.ipynb).

## Discuss what you change to your ER diagram and/or your table implementations. What are some differences between the original design and the final design? Why? What do you think is a more suitable design?

The ER diagram is identical. We felt that all the parameters listed were useful in some way. We also greatly cut down the number of fields from the original CSV file, so we did not need to further remove any fields. This design is highly suitable for the purpose of our application, and we can build off of our current application to enable keyword searches for more fields. 

## Discuss what functionalities you added or removed. Why?

The main functionality we removed was the stored searches. The initial CRUD plan was to create, update, and delete these stored searches while reading from the SQL tables. 

However, we added much more functionality using advanced query and advanced SQL functionality. This includes 4 out-of-the-box search functionality, SQL table CRUD operations, and NLP course-job matching. As stated before, this was done to make the application very simple for the average user and very quick to use. However, going forward, we could add the stored searches back, as that is also a valid approach. 

## Explain how you think your advanced database programs complement your application.

From the students' perspective, students want to gain as much information about the companies, job postings, and courses as they can from our web application. Thus, the advanced queries allow them to do exactly that, as they can obtain different types of information they would be interested in. The NLP helps the keyword search go the extra step with a similarity score. The procedures help with efficiency, and the triggers make realistic changes to the databases after various CRUD operations. Lastly, the transactions are useful when committing the CRUD operations, especially if the app is used by multiple users. This all helps the user experience and allows them to find easy, accurate information. 

## Each team member should describe one technical challenge that the team encountered.  This should be sufficiently detailed such that another future team could use this as helpful advice if they were to start a similar project or where to maintain your project. 

### Rafael:

One challenge I had was coming up with the job description and course-matching mechanism. With so many entries of each, it was not trivial to design a way of matching them that was somewhat efficient and returned good results. I ended up leaning on the content of another class I had taken, CS 410 - Text Information Systems, and borrowed concepts from there. Another more common challenge I faced was ingesting the data from the dataset into the database. Despite the original dataset appearing to have FK constraints, as we discussed above in question 3, it had a lot of inconsistencies, and in many different, subtle ways. Sometimes the FK on a table would refer to an inexistent element on another table, sometimes the FK would point to the incorrect item on another table, and much more. I solved this by creating a Jupyter Notebook analyzing one table at a time, and seeing what the patterns of the inconsistencies were. From there, Realized that many String fields needed to be normalized, so I wrote a function to format strings to PascalCase consistently. This helped tremendously in matching the correct FKs to the correct IDs. I continued the process of identifying the issues with the dataset and writing functions to consistently fix them, and then I processed all the dataset in order of dependencies, and once by one, I ingested the data while not breaking any of our schema’s rules. Please find this Jupyter Notebook [here](https://github.com/cs411-alawini/sp24-cs411-team103-TopDB/blob/main/data/data_ingestion.ipynb) for reference.

### Areet:

Since I have not created a full-stack application, my biggest technical challenge was combining the database, front-end, and API. Although there was a learning curve, I found the process very enjoyable. It helped to use basic HTML to keep the front-end simple. I also used a consistent API structure and designed it well from the beginning, so it would not hurt me later in the process. I also kept the SQL DDL handy so I could easily reference the database. 

### Joey:

When creating the queries, there were a variety of syntax issues that I ran into. In particular, within one of the triggers, there was a syntax error regarding the delimiter that I never included at first. The trigger stated that there were supposed to be two SQL DELETE statements after there was a certain delete on a different table (Companies), and these two DELETE statements were separated by a semicolon. However, when running the trigger in MySQL, an error occurred that stated there was incorrect syntax. This took a while to debug because the SQL trigger seemed completely fine, which it was. It was just missing a DELIMITER // clause immediately before the trigger and a DELIMITER ; clause immediately after the trigger. This allowed the SQL trigger to execute.

### Diego:

I found it overwhelming when I got the information for the indexing when analyzing it. I had to reread it and look carefully at how the cost was being affected. It was important to find the correct indexing for our advanced queries to make sure that the retrieval of the information desired was efficient.

## Are there other things that changed when comparing the final application with the original proposal?

As previously mentioned before, students were going to be suggested classes based on the type of field or job they were interested in. Ultimately, this was later simplified to job searching and using advanced queries for better search results.

## Describe future work that you think, other than the interface, that the application can improve on

The application can be geared more towards its main user-base: students. There can be displays that show job listings, companies, and make it easier for the students to complete keyword search to find the courses and jobs that will set them up for success. In terms of backend, the NLP can be fine tuned to create better recommendations. Additionally, more advanced queries can be added to the procedures, transactions, and triggers to generate better results and functionality for the user. 

## Describe the final division of labor and how well you managed teamwork.

The labor was largely split up among the 4 group members for most of the project. For the final portion, the division was as follows:

### Rafael:

NLP and Keyword Search

### Areet:

Advanced Queries, CRUD, Front-end

### Joey:

Triggers, Procedures, Transactions, Integration with Front-end

### Diego:

Triggers, Procedures, Transactions, Integration with Front-end

