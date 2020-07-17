Language: 
[English](https://github.com/luckysmg/jr_extension/blob/master/README.md) | [中文简体](https://github.com/luckysmg/jr_extension/blob/master/README-CN.md)

# flutter_swipe_action_cell

A package that can give you a cell that can be swiped ,effect is like iOS native

## Why do I want to create this lib?
I like iOS native 's swipe action ,but flutter doesn't give an official widget .
So I try to create one.

## Get started with example


Tip:This widget should be put in the itemBuilder of your ListView

 - Example 1:Simple delete the item in ListView
[](2)

```dart
 SwipeActionCell(
      key: ObjectKey(list[index]),///this key is necessary
      actions: <SwipeAction>[
        SwipeAction(
            title: "delete",
            onTap: (CompletionHandler handler) async {
              list.removeAt(index);
              setState(() {});
            },
            color: Colors.red),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text("this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
```

 - Example 2:Perform first action when full swipe
 
 [](2)
 
 ```dart
 SwipeActionCell(
       ///this key is necessary
       key: ObjectKey(list[index]),
 
       ///this is the same as iOS native
       performsFirstActionWithFullSwipe: true,
       actions: <SwipeAction>[
         SwipeAction(
             title: "delete",
             onTap: (CompletionHandler handler) async {
               list.removeAt(index);
               setState(() {});
             },
             color: Colors.red),
       ],
       child: Padding(
         padding: const EdgeInsets.all(8.0),
         child: Text("this is index of ${list[index]}",
             style: TextStyle(fontSize: 40)),
       ),
     );
 ```

 - Example 3:Delete with animation 
 
 [](3)
 
 ```dart
SwipeActionCell(
      ///this key is necessary
      key: ObjectKey(list[index]),
      ///this name is the same as iOS native
      performsFirstActionWithFullSwipe: true,
      actions: <SwipeAction>[
        SwipeAction(
            title: "delete",
            onTap: (CompletionHandler handler) async {
              list.removeAt(index);
              /// await handler(true) : will delete this row
              ///And after delete animation,setState will called to 
              /// sync your data source with your UI

              await handler(true);
              setState(() {});
            },
            color: Colors.red),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text("this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
 ```

 - Example 4:More than one action: 
 
 [](4)
 
 ```dart
SwipeActionCell(
      ///this key is necessary
      key: ObjectKey(list[index]),

      ///this is the same as iOS native
      performsFirstActionWithFullSwipe: true,
      actions: <SwipeAction>[
        SwipeAction(
            title: "delete",
            onTap: (CompletionHandler handler) async {
              list.removeAt(index);
              await handler(true);
              setState(() {});
            },
            color: Colors.red),
        SwipeAction(
            title: "noAction",
            onTap: (CompletionHandler handler) async {

              ///false means that you just do nothing,it will close
              /// action buttons by default 
              handler(false);
              showCupertinoDialog(
                  context: context,
                  builder: (c) {
                    return CupertinoAlertDialog(
                      title: Text('ok'),
                      actions: <Widget>[
                        CupertinoDialogAction(
                          child: Text('confirm'),
                          isDestructiveAction: true,
                          onPressed: () {
                            Navigator.pop(context);
                          },
                        ),
                      ],
                    );
                  });
            },
            color: Colors.blue),
      ],
      child: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Text("this is index of ${list[index]}",
            style: TextStyle(fontSize: 40)),
      ),
    );
 ```

# About CompletionHandler in onTap function of SwipeAction
it means how you want control this cell after you tap it.
If you don't want any animation,just don't call it and update your data and UI with setState()

If you want some animation:
- hander(true) : Means this row will be deleted(You should call setState after it)

- await handler(true) : Means that you will await the animation to complete(you should call setState after it so that you will get an animation)

- handler(false) : means it will not delete this row.By default,it just close this cell's action buttons.

- handler(false) : means it will wait the close animation to complete.


 


