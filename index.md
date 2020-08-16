[michael.meta125@gmail.com](mailto:michael.meta125@gmail.com) | 
[321.696.9234](tel:3216969234)

# Michael Meta &ndash; Software Developer

## E-Portfolio CS 499

### This E-Portfolio was created to demonstrate my skills in 3 main categories within the Computer Science Scope
  - Software Design & Engineering
  - Data Structures & Algorithms
  - Databases

----
In order to demonstrate proficiency in these 3 areas, I have first picked an artifact related to history within the computer science field, specifically within my current role. This artifact's larger picture is a full landing page, but the partifuclar artifact is centered around a web api with that will return a list of reports. At the end of this artifact, I will also show an example of its use case.

---

## Code Review Video for Planning of Enhancements

[![Code Review](https://img.youtube.com/vi/PH7EcjEd5M8/0.jpg)](https://youtu.be/PH7EcjEd5M8  "Code Review")

----

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

---


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

```
In the above code block, the idea of the service is quickly illustrated. Its job is to return a proper list to the controller. The software design and engineering enhancements show us the importance of decoupling data access and presentation (web api in this case). Data strctures also come into play in this ehancement, as the goal is to have objects that are only related to the application and not necessarily all the information present in the data store. There is no reason to have every attribute of an object stored in a database table most of the time. You can see where we map from the data type object to a data transfer object to be used by the rest of the application. This separation of layers is very helpful as the application grows.

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

As explained a bit in the design and engineering structure, data structures and algorithm proficiency is another area in which I would like to illustrate my knowledge. In the artifact, I would like to first draw attention to the `ValidateReportList()` method. This method was changed further as described in the code review video, for ehancements as well as readbility (cleaning code). Notice the more common scenario within the binary statement is tested first, this means the code runs more efficiently. 

On the data structures side, more changes were made the the repository. Created more LINQ methods which quickly handing filters of the `IEnumerable`. Some slight work was done on the data store side, but more on that later. 

Lastly, change to one of the data structures for a partifular DTO changed. I decided to make a reporting type a second class, this is because I expect the reporting type object to be used for other validation further down the road, so I think this separation will be wise.

The biggest takeaway from this ehancement was using every feature of the IDE. In this case, Visual Studio allowed me to physically see the memory usages of each algorithm as they ran. While the speed difference was minimal, I imagine one day at scale, switching the way the method validated the list, would have a serious performance gain!

---

## Databases

Finally, let us go over the ehancements to the data store.

## Education
**Southern New Hampshire University, NH**  
B.S. in Computer Sciences  
*Heavy STEM*  
*Jan 2020*  

## Skills
- Architectural Pattern &ndash; Data access Layers, UI Layers, Application Layers
- Methodology &ndash; Agile, Scrum, Cross-platform Development, Object-Oriented Programming,     Composition, Rapid Application Development
- Programming Language &ndash; C#, SQL, VB
  - Familiar &ndash; TypeScript, JavaScript, CSS, SASS, HTML
- Data 
   - Familiar &ndash; Schema design, table design, datatype best practices

## Tools
- Framework &ndash;  .Net, .NetCore, ASP.NET, ASP.NET Core, Angular, Node.js, Express, Bootstrap
- Change Control &ndash; GitLab, GitHub
- ORMS &ndash; Entity Framework
- Data &ndash; SQL Server, Oracle, Teradata, Stored Procedures
- Other &ndash; IIS, Docker, Kubernetes, NPM, MSFT Nuget, LINQ

## Experience
**Verizon - Lake Mary, Fl**  
Sys Specialist - System Analysis and Programming  
*September 2018 &ndash; Present*  
- Designed, built, and maintained process to automate access provisioning.
- Multi project solution containing multiple objects for interacting with the Document Object Model through interfaces created.
- Designed, built, and maintained ASP.Net core web APIs to be consumed by applications
  - SQL server job statuses
  - Current Workflow Tool statuses
  - External Weather API
  - Crimson Hexagon Sentient Analysis
- Currently designed Angular application to be used as a team landing page
- Programming lead for worktool application BCA (System Access Tool) - ASP.net
  - Creates new feature and functions - multiple vendor access
  - Debugs and Tests problems and new features
  - Created development application and database for BCA (Original setup was PROD only)
  - Blue Green Deployment (Single IIS) - Limited Downtime when deploying changes

**Verizon - Lake Mary, Fl**  
Sr. Analyst  
*November 2017 &ndash; September 2018*  
- Designed, built, and maintained process which automated ticket distribution for call center reps
- Designed, built, and maintained several integration service packages to automate reporting feed to Tableau
- Designed, built, and maintained UI which worked with call center reps interface to prompt them of customer call rules

**Verizon - Lake Mary, Fl**  
Analyst &ndash;   
*June 2017 &ndash; March 2018*  
- Developed site manager portal which housed tooling used by customer service representatives (Node.js, Styled Components, React, Redux)
- Migrated existing LESS styling to use Styled Components (React, Styled Components, LESS)
- Developed API and Service endpoints (Node.js, Sequelize, Protobuf, Swagger)
- Integrated Auth0 flow into the site manager portal (React, Redux)
- Created wireframes (Balsamiq, InVision)

