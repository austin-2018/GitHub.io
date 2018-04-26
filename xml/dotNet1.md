# WEB SERVICES

#### Web Services Interview Questions | Selected Excerpts
#### https://www.c-sharpcorner.com/UploadFile/sreeelectrons/web-services-interview-questions/

What is a Web Service?

A web service is a web-based functionality accessed using the protocols of the web to be used by the web applications and uses standard XML Messaging for communication.

XML is used to encode all communications to a Web service. For example, a client invokes a Web service by sending an XML message, then waits for a corresponding XML response. Because all communication is in XML, Web services are not tied to any one operating system or programming.

##### What is the namespace for Web Service?

##### System.Web.Services

##### Sample Web Service

##### Creating Service:

##### Create a New ASP.NET Application and add a Web Service.

##### The following example demonstrates a sample web service, which sends information of an Employee. Remember that, we have to use [WebMethod] attribute to expose service method.
using System;  
  
using System.Collections.Generic;  
  
using System.Linq;  
  
using System.Web;  
  
using System.Web.Services;  
  
namespace SampleWebService  
  
{  
  
    /// <summary>  
  
    /// Summary description for Test  
  
    /// </summary>  
  
    [WebService(Namespace = "http://tempuri.org/")]  
  
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
  
    [System.ComponentModel.ToolboxItem(false)]  
  
    // To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line.  
  
    // [System.Web.Script.Services.ScriptService]  
  
    public class Employee  
  
    {  
  
        public int EmpID   
      {  
            get;  
            set;  
        }  
  
        public string EmpName   
        {  
            get;  
            set;  
        }  
  
        public string country   
        {  
            get;  
            set;  
        }  
  
    }  
  
    public class Test: System.Web.Services.WebService  
  
    {  
  
        [WebMethod]  
  
        public Employee GetEmployee()  
  
        {  
  
            return new Employee {  
                EmpID = 1, EmpName = "Sridhar", country = "India"  
            };  
  
        }  
  
    }  
  
}  
