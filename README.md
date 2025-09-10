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

To run the demo, refer to [System Requirements for Xamarin](https://help.syncfusion.com/xamarin/system-requirements)

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
