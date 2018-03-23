# Code-Snippets
依赖属性和附加属性的代码段

依赖属性：

``` CS
/// <summary>
/// 获取或设置MyProperty的值
/// </summary>  
public int MyProperty
{
    get => (int)GetValue(MyPropertyProperty);

    set => SetValue(MyPropertyProperty, value);
}

/// <summary>
/// 标识 MyProperty 依赖属性。
/// </summary>
public static readonly DependencyProperty MyPropertyProperty =
    DependencyProperty.Register(nameof(MyProperty), typeof(int), typeof(MainPage), new PropertyMetadata(default(int), OnMyPropertyChanged));

private static void OnMyPropertyChanged(DependencyObject obj, DependencyPropertyChangedEventArgs args)
{

    var oldValue = (int)args.OldValue;
    var newValue = (int)args.NewValue;
    if (oldValue != newValue)
        return;

    var target = obj as MainPage;
    target?.OnMyPropertyChanged(oldValue, newValue);
}

protected virtual void OnMyPropertyChanged(int oldValue, int newValue)
{
}

```

附加属性：

``` CS
/// <summary>
/// 从指定元素获取 MyProperty 依赖项属性的值。
/// </summary>
/// <param name="obj">从中读取属性值的元素。</param>
/// <returns>从属性存储获取的属性值。</returns>
public static int GetMyProperty(DependencyObject obj) => (int)obj.GetValue(MyPropertyProperty);

/// <summary>
/// 将 MyProperty 依赖项属性的值设置为指定元素。
/// </summary>
/// <param name="obj">对其设置属性值的元素。</param>
/// <param name="value">要设置的值。</param>
public static void SetMyProperty(DependencyObject obj, int value) => obj.SetValue(MyPropertyProperty, value);

/// <summary>
/// 标识 MyProperty 依赖项属性。
/// </summary>
public static readonly DependencyProperty MyPropertyProperty =
    DependencyProperty.RegisterAttached("MyProperty", typeof(int), typeof(MainPage), new PropertyMetadata(default(int), OnMyPropertyChanged));


private static void OnMyPropertyChanged(DependencyObject obj, DependencyPropertyChangedEventArgs args)
{
    var oldValue = (int)args.OldValue;
    var newValue = (int)args.NewValue;
    if (oldValue == newValue)
        return;

    var target = obj as MainPage;
}

```
