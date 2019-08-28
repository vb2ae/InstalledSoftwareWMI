# Get a list of Installed Software using vb or c# and the wmi


# Introduction
Gets a list of Software installed on the local computer 
Building the Sample
Uses Visual Studio 2012 or Visual Studio 2012 Express for Windows Desktop,  The code listed below can be compiled with earlier versions of visual studio, visual basic express edition,  or c# express edition
 
http://www.microsoft.com/visualstudio/eng/downloads
# Description
 
Uses the windows managment interface and visual basic to get a list of the installed installed software on the computer.  The name of the installed software will be displayed in an windows forms list box. You can use the classes in System.Management to query the windows managment interface to get information about the local computer.  In this case we query the Win32_Product class to get the installed software on the computer.   The name property in the returned data is what we will display in a windows form listbox.
The Win32_Product class returns the name, install location, install date, etc..  The Win32_Product class also function for unistalling the software
http://msdn.microsoft.com/en-us/library/windows/desktop/aa394378(v=vs.85).aspx

# C#
```C#
   public partial class Form1 : Form 
    { 
        public Form1() 
        { 
            InitializeComponent(); 
        } 
             
 
    private void LoadSoftwareList() 
    { 
        listBox1.Items.Clear(); 
        ManagementObjectCollection moReturn;   
        ManagementObjectSearcher moSearch; 
 
        moSearch = new ManagementObjectSearcher("Select * from Win32_Product"); 
 
        moReturn = moSearch.Get(); 
       foreach(ManagementObject mo in moReturn) 
       { 
           listBox1.Items.Add(mo["Name"].ToString()); 
       } 
 
    } 
 
 
        private void Form1_Load(object sender, EventArgs e) 
        { 
            LoadSoftwareList(); 
        }
```

# Visual Basic
```Visual Basic
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load 
        LoadSoftwareList() 
    End Sub 
 
    Private Sub LoadSoftwareList() 
        ListBox1.Items.Clear() 
        Dim moReturn As Management.ManagementObjectCollection 
        Dim moSearch As Management.ManagementObjectSearcher 
        Dim mo As Management.ManagementObject 
 
        moSearch = New Management.ManagementObjectSearcher("Select * from Win32_Product") 
 
        moReturn = moSearch.Get 
        For Each mo In moReturn 
            ListBox1.Items.Add(mo("Name").ToString) 
        Next 
 
    End Sub
```


# More Information

http://msdn.microsoft.com/en-us/library/windows/desktop/aa394378(v=vs.85).aspx

http://social.msdn.microsoft.com/Forums/en-US/vbgeneral/thread/7159b57c-f6a8-4a6a-ab8c-dd65f4d7973a/
