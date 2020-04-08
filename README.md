# How to bind command in Xamarin.Forms Accordion (SfAccordion)

You can bind the ViewModel [commands](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/commanding) to content of [AccordionItem](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Accordion.AccordionItem.html?) in Xamarin.Forms [SfAccordion](https://help.syncfusion.com/xamarin/accordion/getting-started?).

You can also refer the following article.

https://www.syncfusion.com/kb/11359/how-to-bind-command-in-xamarin-forms-accordion-sfaccordion

**C#**

ViewModel command to show the Accordion details.

``` c#
namespace AccordionXamarin
{
    public class ItemInfoRepository
    {
        public Command<object> ShowDetailsCommand { get; set; }
        public ItemInfoRepository()
        {
            ShowDetailsCommand = new Command<object>(OnShowDetailClicked);
        }
        
        private void OnShowDetailClicked(object obj)
        {
            var item = obj as ItemInfo;
            App.Current.MainPage.DisplayAlert(item.Name, item.Description, "Ok");
        }
    }
}
```

**XAML**

Binding the ViewModel command to the [ImageButton](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/imagebutton) that is loaded inside the [content](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Accordion.AccordionItem~Content.html?) of AccordionItem.

``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:AccordionXamarin"
             xmlns:accordion="clr-namespace:Syncfusion.XForms.Accordion;assembly=Syncfusion.Expander.XForms"
             x:Class="AccordionXamarin.MainPage">
 
    <ContentPage.BindingContext>
        <local:ItemInfoRepository x:Name="viewModel"/>
    </ContentPage.BindingContext>
 
    <accordion:SfAccordion x:Name="accordion" BindableLayout.ItemsSource="{Binding Info}" ExpandMode="SingleOrNone">
        <BindableLayout.ItemTemplate>
            <DataTemplate>
                <accordion:AccordionItem>
                    <accordion:AccordionItem.Header>
                        <Grid Padding="5,0,0,0" HeightRequest="50">
                            <Label Text="{Binding Name}" FontSize="20" />
                        </Grid>
                    </accordion:AccordionItem.Header>
                    <accordion:AccordionItem.Content>
                        <Grid BackgroundColor="LightGray" Padding="5,0,0,0">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="*" />
                                <ColumnDefinition Width="45" />
                            </Grid.ColumnDefinitions>
                            <Label Text="{Binding Description}" VerticalOptions="Center"/>
                            <Grid Grid.Column="1" Padding="10" BackgroundColor="LightGray">
                                <ImageButton HeightRequest="30" WidthRequest="30" Source="Details.png" Command="{Binding Path=BindingContext.ShowDetailsCommand, Source={x:Reference accordion}}" CommandParameter="{Binding .}"/>
                            </Grid>
                        </Grid>
                    </accordion:AccordionItem.Content>
                </accordion:AccordionItem>
            </DataTemplate>
        </BindableLayout.ItemTemplate>
    </accordion:SfAccordion>
</ContentPage>
```
