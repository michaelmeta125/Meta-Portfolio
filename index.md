[michael.meta125@gmail.com](mailto:michael.meta125@gmail.com) | 
[321.696.9234](tel:3216969234)

# Michael Meta &ndash; Software Developer

## E-Portfolio CS 499

### Self Reflection

Throughout my computer science courses I have built great proficiency in many areas. This e-portfolio is meant to demonstrate those proficiencies. I am already employed as a junior software developer at a large company, and these courses have given me a greater understanding of some of the key princples of this field. For example, prior to this course work I had never touched a noSQL database. Throughout my client server development course, I was able to use MongoDB and Python to create a REST API. Prior to this course, I would never have been able to explain noSQL options to a potential employer, and now I can speak to it, I can implement it as well.

While I used GitLab daily at my current job, taking the team project course in the computer science program allowed me to understand the why behind Git methodologies. Sure I knew how to create a branch and merge it back, but some of the key pieces of Git I was missing. Something as simple as `stash` I never even went to checkout (pun intended) because I had no formal training on why it could be useful. I also like how this course demonstrate how to work on a team within the same project, and at times, same exact codebase, and even the same exact code file. I became more efficient in Git, and can also add BitBucket to my resume. Before I only could speak to Gitlab and Github.

The code review process within this specific course was very helpful in communicating to stake holders. While we had done code reviews in other courses, the video code review was very important to me. I realize a code review is a technical video, but it taught me how to speak to each item in simpler terms that a stake holder could understand. I think sometimes I get caught up in speaking too much in a way that I understand, but recording myself in a video, gave me that opportunity to speak like a human to someone. More than that, I would rewatch my code review, and it kept me less confused on what to tackle next. It is funny how much I will look at code a month later, and then confuse myself, but I have my explanation in video form :).

My proficiency in data structures and alorithms began in my Python course. While we were not trying to become masters in Python, the goal was the fundamentals. This is a `string` this is an `int` etc. These fundamentals keep moving with you throughout the computer science program. Boot camps are for becoming a mastery in the language as is practice, but I felt the courses in this program were meant to get the fundamentals into our brains. We would create `if` statements in python to understand how to get our alorithms from point A to B and return the proper value we desired based on criteria. All of this can be applied to a vast number of languages.

I mentioned the different databases I became familiar with throughout this course, most notably MongoDB and MySQL, but also importantly was engineering them in an efficient way. In my computer science course we learning how to put indexes in the MySQL database. We were then given queries to run, and it was clear the differences in run efficiences. This particular learning experience brought me back into work, and the DBAs often did not have to edit my tables nearly as much as before. I would be able to create tables that were specifically made for fast inserts updates and deletes. Indexes are so simple to me now, and just another way I have become more proficient in creating a database for my applications.

One thing I neglected to mention was in regards to security. While this particular application (artifact) will be on a Windows Macchine and security will be controlled with ADOM groups, the Linux course I took really gave me a better understanding of how to create structure for the application files with security on Linux, which I think it is important to be able to speak to. So because of the modular way Linux is setup, you can more easily limit the users. For example with Windows, there are so many items a users will need to be able to have privileges too just for a specific application to run properly. This can be insecure compared to Linux, which the course greatly highlighted.


### This E-Portfolio was created to demonstrate my skills in 3 main categories within the Computer Science Scope
  - Software Design & Engineering
  - Data Structures & Algorithms
  - Databases

----
In order to demonstrate proficiency in these 3 areas, I have first picked an artifact related to history within the computer science field, specifically within my current role. This artifact's larger picture is a full landing page, but the partifuclar artifact is centered around a web api with that will return a list of reports. At the end of this artifact, I will also show an example of its use case.

## Artifact Full Review & Description

The artifact in this enhancement section is a compilation of a few things requested April of 2020. While the project as a whole is to develop a landing page. The specific items for the artifact are, data store (database table specifically for this report part), web API accessed via HTTP (return results in JSON format), service layer that communicates with a set of data access repositories. The specific report item needed to have a table with all the reports that is securely returned to our controllers and finally serialized to JSON and returned to the client(s). The artifact was required to use a few technologies. 

- Back end - .net core web APIs (Language C#)
- Front End – React
- Data store – SQL Server 2016

I selected this item for a few reasons. The most important is because it is an active project I am working on. Granted, some of the data will either be masked or changed because it is confidential, this artifact should illustrate proficiency in the three areas I have spelled out above. I think a project like this can show case all skills. From knowledge of the data store, to understanding of React and other highly effective JavaScript frameworks, and of course knowledge of REST APIs, and this effectively demonstrates knowledge with that. I think the main goal this artifact highlights is software design and utilizing well known patterns and tools. For example, the decoupling of the data access project via repository and services and unit of work is quite a common design for testability and reusability. [Read More On Repository Pattern](https://medium.com/@mlbors/using-the-repository-pattern-with-the-entity-framework-fa4679f2139)

To summarize, the code review explains the ehancements and fixes to the artifact to properly demonstrate 

 - Software Design & Engineering (eg: Web API, Repository Pattern)
 - Data Structures and Alogirithms (eg: POCO - DTO, LINQ)
 - Databases (eg: SQL Server Data Store Table)
  
I would also like to point out the video was a good example of proficiency in code review, which I believe is a fundamental piece of the software design and engineering category. Code review is very important, and it might not just be to catch bugs or mistakes, you may even catch inefficiences, as you can see with my `if{}` statements in the `list()` creation.

Finally, I would like to explain why this artifact as a whole is a great way to demonstrate proficiency in all 3 categories. I think it was great to be able to choose an artifact that is comprised of all pieces of these categories. The reason being is that we can see full circle how the data store feeds the backend and how the backend can be access from something like an Angular front end via HTTP. Separate artifacts would have worked too, and I somewhat called them separate, but in general, it all is one large artifact. 

Data store -> Backend -> Frontend (Client)

---

## Code Review Video for Planning of Enhancements

[![Code Review](https://img.youtube.com/vi/PH7EcjEd5M8/0.jpg)](https://youtu.be/PH7EcjEd5M8  "Code Review")

----



## Software Design & Engineering

Below I will show the code changes made and the design used. 

*Note interaction with these items will be shown later*

```
 public class ReportService:IReportService
    {
        IUnitOfWork _unitOfWork;
        IMapper _mapper;
        public ReportService(IUnitOfWork unitOfWork,IMapper mapper)
        {
            _unitOfWork = unitOfWork;
            _mapper = mapper;
        }
        /// <summary>
        /// Uses auto mapper to map and return list of report objects
        /// </summary>
        /// <returns></returns>
        public IEnumerable<Report> GetAllReports()
        {
            var reportList = _mapper.Map<List<Report>>(_unitOfWork.ReportingLinkRepository.GetAll());
            if(ValidateReportList(reportList) == true)
            {
                return reportList;
            }
            return null;
        }
        public IEnumerable<Report> GetAllActiveReports(DateTime currentDate)
        {
            var reportList = _mapper.Map<List<Report>>(_unitOfWork.ReportingLinkRepository.GetAllActiveReports(currentDate));
            if (ValidateReportList(reportList) == true)
            {
                return reportList;
            }
            return null;
        }
        /// <summary>
        /// Verifies there are reports to provide a list of
        /// </summary>
        /// <param name="reports"></param>
        /// <returns></returns>
        private bool ValidateReportList(List<Report> reports)
        {
            return (reports.Count.Equals(0));
        }
    }

     [Route("api/[controller]")]
    [ApiController]
    public class ReportingController : ControllerBase
    {

        /// <summary>
        /// DI setup for class services
        /// </summary>
        private IReportService _services;

        public ReportingController(IReportService services)
        {
            _services = services;
        }
        /// <summary>
        /// Route that will return all reports
        /// </summary>
        /// <returns></returns>
        [HttpGet]
        [Route ("GetAllReports")]
        public ActionResult<IEnumerable<Report>> GetAllReports()
        {
            return Ok(_services.GetAllReports());
        }
        /// <summary>
        /// Route that will return only active reports as specified by the date provided
        /// </summary>
        /// <returns></returns>
        [HttpGet]
        [Route("GetActiveReports")]
        public ActionResult<IEnumerable<Report>> GetActiveReports()
        {
            return Ok(_services.GetAllActiveReports(DateTime.Now));
        }
    }

```

The artifact in this enhancement section is a compilation of a few things request April 2020. While the project as a whole is to develop a landing page. The specific items for the artifact are, data store (database table specifically for this report part), web API accessed via HTTP (return results in JSON format), service layer that communicates with a set of data access repositories. The specific report item need to have a table with all the reports that is securely returned to our controllers and finally serialized to JSON and returned to the client(s). The artifact was required to use a few technologies. 

In the above code block, the idea of the service is quickly illustrated. Its job is to return a proper list to the controller. The software design and engineering enhancements show us the importance of decoupling data access and presentation (web api in this case). Data strctures also come into play in this ehancement, as the goal is to have objects that are only related to the application and not necessarily all the information present in the data store. There is no reason to have every attribute of an object stored in a database table most of the time. You can see where we map from the data type object to a data transfer object to be used by the rest of the application. This separation of layers is very helpful as the application grows.

Also in the above code block, we can see this separation of layers by looking at the controller class. This class was created with the design princples explained above about properly decoupling different aspects of the applcation. The controller also sticks with the single respsonibility, it listens and handles the request, and returns the data. The only logic that would be inside the controller in this scenario would be server codes. Currently, we are returning 201, but in future development, there would be different codes that could be returned so the client can handle them appropriately. You can also see in this code block the addition of that other `Route`. This route is for all active reports, which will bring us full circle when we see the service methods and the updates to the repository's methods. More importantly, the new controller method demonstrates the completion of another aspect of the planned ehancements from the code review video.

The main takeaway from this enhancement was the value of code review. As I stated, I was very used to writing code and shooting it off for review. However, by having a written checklist that I run through with every piece of code I write, I was able to find inefficiences. The validation method is a perfect example of that. You can imagine in another person's code review, they may compile and notice everything checks out and the code does what it says it will do, but what if they do not catch issues related to efficiency. Better I review it with a checklist first, and have that much better chance to catch those issues.

---

## Datastructures & Algorithms

As with software design & engineering enhancements, let us take a look at the data structure and algorithm code ehancements, and then explain.

```
 public class ReportingLinkRepository : Repository<ReportingLink>, IReportingLinkRepository
    {
        public ReportingLinkRepository(LandingPageContext context)
            : base(context)
        {
        }
        /// <summary>
        /// Get all active reports implmeents from interface Will pull list of all reports with active dates
        /// </summary>
        /// <returns></returns>
        public IEnumerable<ReportingLink> GetAllActiveReports(DateTime currentDate)
        {
            return _context.Set<ReportingLink>().Where(x => x.EndDate == null || x.EndDate >= currentDate).ToList();
        }
    }


  /// <summary>
        /// Verifies there are reports to provide a list of
        /// </summary>
        /// <param name="reports"></param>
        /// <returns></returns>
        private bool ValidateReportList(List<Report> reports)
        {
            return (reports.Count.Equals(0));
        }

 public class Report
    {
        public string Name { get; set; }
        public string Location { get; set; }
        public ReportingType ReportingType { get; set; }

    }
    public class ReportingType
    {
        public string Type { get; set; }
        public string FunctionName { get; set; }
    }

```

Reiterate for context:

The artifact in this enhancement section is a compilation of a few things request April 2020. While the project as a whole is to develop a landing page. The specific items for the artifact are, data store (database table specifically for this report part), web API accessed via HTTP (return results in JSON format), service layer that communicates with a set of data access repositories. The specific report item need to have a table with all the reports that is securely returned to our controllers and finally serialized to JSON and returned to the client(s). The artifact was required to use a few technologies. 

As explained a bit in the design and engineering structure, data structures and algorithm proficiency is another area in which I would like to illustrate my knowledge. In the artifact, I would like to first draw attention to the `ValidateReportList()` method. This method was changed further as described in the code review video, for ehancements as well as readbility (cleaning code). Notice the more common scenario within the binary statement is tested first, this means the code runs more efficiently. 

On the data structures side, more changes were made the the repository. Created more LINQ methods which quickly handing filters of the `IEnumerable`. Some slight work was done on the data store side, but more on that later. 

Lastly, change to one of the data structures for a partifular DTO changed. I decided to make a reporting type a second class, this is because I expect the reporting type object to be used for other validation further down the road, so I think this separation will be wise.

This part of the artifact was important to add, because while I have made certain touches and changes to all aspects of the application as I have been going each week, I have given most focus to the subject at hand. In the data structures and algorithms, I have spent many hours trying to figure out the best way to narrow down the IEnumerable’s result set, and I think I came up with a fast solution with these changes. I think this also really helps illustrate my knowledge of using collections. I have seen some pretty slick ways to do some of this in other languages too, but I think this was showing an “ok” way. 

The biggest takeaway from this ehancement was using every feature of the IDE. In this case, Visual Studio allowed me to physically see the memory usages of each algorithm as they ran. While the speed difference was minimal, I imagine one day at scale, switching the way the method validated the list, would have a serious performance gain!

---

## Databases

To see the ehancements in code form, we can take a look at the EF Migration code. I have also added the data object's classes.

```
 protected override void Up(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.CreateTable(
                name: "Alerts",
				schema: "Alert",
                columns: table => new
                {
                    Guid = table.Column<Guid>(nullable: false),
                    EffectiveDate = table.Column<DateTime>(nullable: false),
                    EndDate = table.Column<DateTime>(nullable: true),
                    DateAdded = table.Column<DateTime>(nullable: false),
                    AddedBy = table.Column<string>(nullable: false),
                    DateModified = table.Column<DateTime>(nullable: true),
                    ModifiedBy = table.Column<string>(nullable: true),
                    Id = table.Column<int>(nullable: false),
                    HeaderMessage = table.Column<string>(nullable: true),
                    DetailedMessage = table.Column<string>(nullable: true),
                    PriorityLevel = table.Column<string>(nullable: true),
                    NotificationActive = table.Column<DateTime>(nullable: false)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_Alerts", x => x.Guid);
                });

            migrationBuilder.CreateTable(
                name: "ReportingLinks",
				schema: "Reports",
                columns: table => new
                {
                    Guid = table.Column<Guid>(nullable: false),
                    EffectiveDate = table.Column<DateTime>(nullable: false),
                    EndDate = table.Column<DateTime>(nullable: true),
                    DateAdded = table.Column<DateTime>(nullable: false),
                    AddedBy = table.Column<string>(nullable: false),
                    DateModified = table.Column<DateTime>(nullable: true),
                    ModifiedBy = table.Column<string>(nullable: true),
                    LinkId = table.Column<int>(nullable: false),
                    TypeOfReport = table.Column<string>(nullable: true),
                    FunctionOfReport = table.Column<string>(nullable: true),
                    LinkAddress = table.Column<string>(nullable: true),
                    LinkDescription = table.Column<string>(nullable: true),
                    ReportName = table.Column<string>(nullable: true),
                    ContactEmail = table.Column<string>(nullable: true),
                    ContactName = table.Column<string>(nullable: true)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_ReportingLinks", x => x.Guid);
                });
        }

        protected override void Down(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.DropTable(
                name: "Alerts");

            migrationBuilder.DropTable(
                name: "ReportingLinks");
        }

            public class ReportingLink:BaseDataModel,IEntity
    {
        public int LinkId { get; set; }
        public string TypeOfReport { get; set; }
        public string FunctionOfReport { get; set; }
        public string LinkAddress { get; set; }
        public string LinkDescription { get; set; }
        public string ReportName { get; set; }
        public string ContactEmail { get; set; }
        public string ContactName { get; set; }
    }
}

```
Reiterate for context:

The artifact in this enhancement section is a compilation of a few things request April 2020. While the project as a whole is to develop a landing page. The specific items for the artifact are, data store (database table specifically for this report part), web API accessed via HTTP (return results in JSON format), service layer that communicates with a set of data access repositories. The specific report item need to have a table with all the reports that is securely returned to our controllers and finally serialized to JSON and returned to the client(s). The artifact was required to use a few technologies. 

Finally, let us go over the ehancements to the data store. During the code review, you can see the table's column's data types were not well thought out from a memory perspective. All of them were using the default values, and in most cases even when we knew the data would be a string of seven, we still allowed for SQL Server to be ready to except `MAX`. Also, no indexes were on this table. Queries ran slow and SQL Server could not create its plan accordingly. Lastly, no schema was recognizable. The table was in a mess of other tables, but creating a schema for it, we were able to better organize the database.

The ehancements were made using Entity Framework Core. This library allows for a code first design, and allowed for easy migrations to the data store. It is generally the most widely used ORM when using SQL Server. You can read more about [Entity Framework](https://docs.microsoft.com/en-us/ef/core/).

The objective was met in this ehancement section because the data store was corrected for efficiences, and the best part, I was able to show proficiency in the use of EF Core 3+. The column types were changed for proper memory usage, indexes were added to make queries faster as well.

My biggest take away from this section was understanding speed and efficiency increases when using indexes in SQL Server. When the table is small (few rows) queries might not be affected by inefficiences. However, as the data grows the table grows, and without indexes, SQL Server would be slower to return queries. Slower queries means bad application performance and ultimately in this case a slow web API that clients would not want to use.

# Now... What You Have All Been Waiting To Click!

## The following is the artifact as a whole.

### To Review...

- We have created a data store table
- We have created a backend to access this data
- We have created an example of how to display this data

Proficiency in the 3 categories was met.

- Software Design & Engineering
  - Repository Pattern
  - Separation of Layers
  - Controllers and Routes with Single Responsibility

- Data Structures & Algorithms
  - Plain Old CLR Objects Mapped to Data Transfer Objects
  - LINQ for Faster List Filters
  - Report Validation Method Logical Change for Efficiency


- Databases
  - SQL Server Table
  - Indexes Added for Query Efficiency
  - Data Column Types Changed to Match Data & Data Size

While the display of the data was not necessarily touched on in this project... as a whole, my goal was to ultimately demonstrate how a client might use the application created.

We will show an Angular front end, requesting an endpoint which our application is listening on.
