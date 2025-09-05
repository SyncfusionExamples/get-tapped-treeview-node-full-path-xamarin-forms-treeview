# get-tapped-treeview-node-full-path-xamarin-forms-treeview

This example demonstrates how to retrieve the full hierarchical path of a tapped node in the Syncfusion Xamarin.Forms TreeView (SfTreeView) control. The sample shows how to handle node tap events, traverse parent nodes programmatically, and assemble the complete path from the root to the selected node.

## Sample

### XAML
```xaml
<ContentPage.BindingContext>
    <local:FileManagerViewModel x:Name="viewModel"/>
</ContentPage.BindingContext>
<ContentPage.Content>
    <syncfusion:SfTreeView x:Name="treeView"
                         ItemHeight="40"
                         Indentation="15"
                         ExpanderWidth="40"
                           TapCommand="{Binding TappedCommand}"
                         SelectionMode="Single"
                         ChildPropertyName="SubFiles"
                         ItemsSource="{Binding ImageNodeInfo}"
                         AutoExpandMode="AllNodesExpanded">
            ...
    </syncfusion:SfTreeView>
</ContentPage.Content>
```

### ViewModel
```csharp
public class FileManagerViewModel
{
    private Command<Object> tappedCommand;

    public FileManagerViewModel()
    {
        TappedCommand = new Command<object>(TappedCommandMethod);
    }

    public Command<object> TappedCommand
    {
        get { return tappedCommand; }
        set { tappedCommand = value; }
    }

    private void TappedCommandMethod(object obj)
    {
        string nodepath = GetNodePath(obj as Syncfusion.TreeView.Engine.TreeViewNode);
        App.Current.MainPage.DisplayAlert("Path ", nodepath, "Ok");
    }
        public string GetNodePath(Syncfusion.TreeView.Engine.TreeViewNode node)
    {
        string fullpath = "";
        string path = "";
        while (node != null)
        {
            path = @"\" + (node.Content as FileManager).ItemName;
            if (node.ParentNode != null)
            {
                node = node.ParentNode;
            }
            else
            {
                node = null;
            }
            fullpath = path + fullpath;
        }
        return fullpath;
    }
}
```

## Requirements to run the demo
Visual Studio 2017 or Visual Studio for Mac.
Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.