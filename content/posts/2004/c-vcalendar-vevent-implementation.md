---
title: "C# VCalendar/VEvent Implementation"
date: 2004-04-27
---
Here is a class that outputs a valid vCalendar string.  Again, not all
of the spec is implemented here since I was targeting Outlook. 
Everything that is here is all that Outlook supports (according to my
findings)

```csharp
Hope it comes in handy:

     using System;
     using System.Text;
     using System.IO;
     using System.Collections;
    
     namespace TT.Utility
     {
         /// <summary>
         /// Summary description for vEvent.
        /// </summary>
        public class VEvent
        {
            private DateTime _dateCreated = DateTime.Now;
            private DateTime _endDateTime;
            private DateTime _startDateTime;
            public ArrayList Categories = new ArrayList();
            public ClassificationType Classification =
ClassificationType.PUBLIC;
            
            private int _priority = 0;
   
            private string _subject = "";
            private string _description = "";
            
            #region Public Constructors
            public VEvent()
            {
   
            }
            
            public VEvent(string subject, string description,
DateTime startDateTime, DateTime endDateTime)
            {
                _subject = subject;
                _description = description;
                _startDateTime = startDateTime;
                _endDateTime = endDateTime;
            }
   
            public VEvent(string subject, string description,
DateTime startDateTime, DateTime endDateTime, int priority)
            {
                _subject = subject;
                _description = description;
                _priority = priority;
                _startDateTime = startDateTime;
                _endDateTime = endDateTime;
            }
   
            public VEvent(string subject, string description,
DateTime startDateTime, TimeSpan meetingLength)
            {
                _subject = subject;
                _description = description;
                _startDateTime = startDateTime;
                _endDateTime = startDateTime.Add(meetingLength);
            }
   
            public VEvent(string subject, string description,
DateTime startDateTime, TimeSpan meetingLength, int priority)
            {
                _subject = subject;
                _description = description;
                _priority = priority;
                _startDateTime = startDateTime;
                _endDateTime = startDateTime.Add(meetingLength);
            }
   
            #endregion
            
            public void Generate(string filePath, FileMode mode)
            {
                FileStream fs = new FileStream(filePath, mode);
   
                Generate(fs);
            }
   
            public void Generate(Stream outputStream)
            {
                StreamWriter sw = new StreamWriter(outputStream);
   
                using (sw)
                {
                    sw.Write(this.ToString());
                }
            }
   
            public override string ToString()
            {
                StringBuilder sb = new StringBuilder();
                
                //Start the event
                sb.Append("BEGIN:VCALENDARrn");
                sb.Append("VERSION:1.0rn");
                sb.Append("BEGIN:VEVENTrn");
                
                //Add the date created
                sb.Append("DCREATED: " +
_dateCreated.ToUniversalTime().ToString("yyyyMMddTHHmmssZ") +
"rn");
                
                sb.Append("DTSTART: " +
_startDateTime.ToUniversalTime().ToString("yyyyMMddTHHmmssZ") +
"rn");
                sb.Append("DTEND: " +
_endDateTime.ToUniversalTime().ToString("yyyyMMddTHHmmssZ") +
"rn");
   
                sb.Append("PRIORITY: " + _priority + "rn");
   
               sb.Append("SUMMARY: " + _subject + "rn");
               sb.Append("DESCRIPTION: " + _description +
"rn");
  
               if( Categories.Count != 0 )
               {
                   sb.Append("CATEGORIES: ");
                   foreach(string category in Categories)
                   {
                       sb.Append( category + ";" );
                   }
                   sb.Append( "rn" );
               }
  
               sb.Append("CLASS:" +
Enum.GetName(typeof(ClassificationType), Classification) + "rn" );
  
               //End the event
               sb.Append("END:VEVENTrn");
               sb.Append("END:VCALENDARrn");
  
               return sb.ToString();
           }
           
           /// <summary>
           /// DateTime that the vEvent was created. Not required.
           ///Defaults to current date and time.
           /// </summary>
           public DateTime DateCreated
           {
               get
               {
                   return _dateCreated;
               }
  
               set
               {
                   _dateCreated = value;
               }
           }
  
           /// <summary>
           /// DateTime that the vEvent will be done.
           /// </summary>
           public DateTime EndDateTime
           {
               get
               {
                   return _endDateTime;
               }
  
               set
               {
                   _endDateTime = value;
               }
           }
  
           /// <summary>
           /// DateTime that the vEvent will start.
           /// </summary>
           public DateTime StartDateTime
           {
               get
               {
                   return _startDateTime;
               }
  
               set
               {
                   _startDateTime = value;
               }
           }
  
           /// <summary>
           /// Any valid Int32. 0 is undefined. 1 is High Priority.
           ///-1 is Low Priority. Defaults to 0.
           /// </summary>
           public int Priority
           {
               get
               {
                   return _priority;
               }
  
               set
               {
                   _priority = value;
               }
           }
  
           /// <summary>
           /// Subject of the vEvent
           /// </summary>
           public string Subject
           {
               get
               {
                   return _subject;
               }
  
               set
               {
                   _subject = value;
               }
           }
  
           /// <summary>
           /// Description of the vEvent
           /// </summary>
           public string Description
           {
               get
               {
                   return _description;
               }
  
               set
               {
                   _description = value;
               }
           }
       }
  
       public enum ClassificationType
       {
           PUBLIC,
           PRIVATE,
           CONFIDENTIAL
       }
   }
```
