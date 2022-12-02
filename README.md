# Introduction
As part of the Software Developer Boot Camp at The Tech Academy, I was able to work on a Live Project for C# and the .NET Framework for two weeks. For this project specifically, we utilized ASP.NET MVC and Entity Framework, with a code-first database. We also used Bootstrap for the front end. The goal of the project was to help develop a website for a theater production company based in Oregon. The website was to be designed such that the theater company could easily manage their company needs, such as accepting and keeping track of equipment rentals and donations, managing subscriber information, and other related services. For my part, I was mainly tasked with implementing CRUD functionality to keep track of both equipment rental requests as well as a history of equipment rentals. I was also tasked with styling and improving the user experience for these pages on the front end as well.

Throughout our time on the project, we practiced the Agile/Scrum methodology. As part of this process, each student was assigned user stories. Similar to the Python Live Project that I also participated in, these stories gave us specific tasks to accomplish in order to aid in the creation of this website. The stories were all viewable on Azure DevOps, which we used to coordinate our efforts. It is important to note that we were not explicitly told how to actually accomplish each story, and needed to do some measure of outside research and individual testing in order to complete our tasks. The purpose of this was to facilitate learning, and as such I feel that it was very helpful for me.

Below I have included parts of code I actually wrote while on this project, along with explanations of how and why I implemented each feature.

# Back-End
- ## Entity Models
  During my time on the project, I had to create two seperate entity models (utilizing the Entity framework): one for keeping track of equipment rental requests,     and another for keeping a history of equipment rentals and any pertinent information. The models I created are shown below.
  
  Here is the model for rental requests:
  
  ```
  namespace TheatreCMS3.Areas.Rent.Models
  {
    public class RentalRequest
    {
        public int RentalRequestID { get; set; }
        public string ContactPerson { get; set; }
        public string Company { get; set; }
        public DateTime RequestedTime { get; set; }
        public DateTime StartTime { get; set; }
        public DateTime EndTime { get; set; }
        public string ProjectInfo { get; set; }
        public int RentalCode { get; set; }
        public bool Accepted { get; set; }
        public bool ContractSigned { get; set; }
    }
  }
  ```

  Here is the model for Rental History:

  ```
  namespace TheatreCMS3.Areas.Rent.Models
  {
      public class RentalHistory
      {
          public int RentalHistoryId { get; set; }
          public bool RentalDamaged { get; set; }
          public string DamagesIncurred { get; set; }
          public string Rental { get; set; }
      }
  }
  ```
  
  After this was done, all I needed to do was add my new models to the IdentityModels.cs file for the project:
  
  ```
  public System.Data.Entity.DbSet<TheatreCMS3.Areas.Rent.Models.RentalRequest> RentalRequests { get; set; }
  ```
  
  ```
  public System.Data.Entity.DbSet<TheatreCMS3.Areas.Rent.Models.RentalHistory> RentalHistory { get; set; }
  ```
  
  Then, once I built and ran the project, database tables were automatically created based on these models. This would allow us to keep track of the information and   store it for retrieval later.
  
- ## CRUD Pages/Functionality
  After creating the entity models, I needed to scaffold the CRUD pages using Entity Framework. As part of this process, I was given instructions to use the Layout   file for the site, which was created beforehand. After scaffolding the pages, I was left with a create, edit, details, delete, and index page for both Rental       Requests and Rental History. Here is an example of a scaffolded Rental History details page:
  
  ```
  @model TheatreCMS3.Areas.Rent.Models.RentalHistory

  @{
    ViewBag.Title = "Details";
    Layout = "~/Views/Shared/_Layout.cshtml";
  }

  <h2>Details</h2>

  <div>
      <h4>RentalHistory</h4>
      <hr />
      <dl class="dl-horizontal">
          <dt>
              @Html.DisplayNameFor(model => model.RentalDamaged)
          </dt>

          <dd>
              @Html.DisplayFor(model => model.RentalDamaged)
          </dd>

          <dt>
              @Html.DisplayNameFor(model => model.DamagesIncurred)
          </dt>

          <dd>
              @Html.DisplayFor(model => model.DamagesIncurred)
          </dd>

          <dt>
              @Html.DisplayNameFor(model => model.Rental)
          </dt>

          <dd>
              @Html.DisplayFor(model => model.Rental)
          </dd>

      </dl>
  </div>
  <p>
      @Html.ActionLink("Edit", "Edit", new { id = Model.RentalHistoryId }) |
      @Html.ActionLink("Back to List", "Index")
  </p>
  ```
  
  By now, I had implemented both the models, as well as created CRUD pages for each of them. At this point, these pages were fully functional, and were able to create, read, update, and delete items from the database. After creating the models and scaffolding the views, I was also tasked with styling the front end to make it more attractive and create a better user experience.
  
# Front-End
- ## Rental Requests
  I was eventually tasked with making the Rental Requests Index page look better by turning the default display into an accordion. To do this, I needed to 
  
  
