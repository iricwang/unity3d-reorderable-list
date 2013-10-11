README
======

List control for Unity allowing editor developers to add reorderable list controls to
their GUIs. Supports generic lists and serialized property arrays, though additional
collection types can be supported by implementing `Rotorz.ReorderableList.IReorderableListAdaptor`.

Use of this source code is governed by a BSD-style license that can be found in
the LICENSE file.

![screenshot](https://bitbucket.org/rotorz/reorderable-list-editor-field-for-unity/raw/master/screenshot.png)

Features
--------

- Drag and drop reordering!
- Easily customized using flags.
- Adaptors for `IList<T>` and `SerializedProperty`.
- Subscribe to add/remove item events.
- Supports mixed item heights.
- Disable drag and/or removal on per-item basis.
- Styles can be overriden on per-list basis if desired.
- Subclass list control to override context menu.
- API reference documentation (Asset Path/Support/API Reference.chm).

Installing scripts
------------------

This control can be added to your project by importing the Unity package which
contains a compiled class library (DLL). This can be used by C# and UnityScript
developers.

[Download RotorzReorderableList_v0.2.2 Package (requires Unity 4.2.1+)](<https://bitbucket.org/rotorz/reorderable-list-editor-field-for-unity/downloads/RotorzReorderableList_v0.2.2.unitypackage>)

If you would prefer to use the non-compiled source code version in your project,
copy the contents of this repository somewhere into your project.

**Note to UnityScript (*.js) developers:**

UnityScript will not work with the source code version of this project unless
the contents of this repository is placed at the path "Assets/Plugins/ReorderableList"
due to compilation ordering.

Example 1: Serialized array of strings (C#)
-------------------------------------------

    :::csharp
    SerializedProperty _wishlistProperty;
    SerializedProperty _pointsProperty;

    void OnEnable() {
        _wishlistProperty = serializedObject.FindProperty("wishlist");
        _pointsProperty = serializedObject.FindProperty("points");
    }

    public override void OnInspectorGUI() {
        serializedObject.Update();

        ReorderableListGUI.Title("Wishlist");
        ReorderableListGUI.ListField(_wishlistProperty);

        ReorderableListGUI.Title("Points");
        ReorderableListGUI.ListField(_pointsProperty, ReorderableListFlags.ShowIndices);

        serializedObject.ApplyModifiedProperties();
    }

Example 2: List of strings (UnityScript)
----------------------------------------

    :::javascript
    var yourList:List.<String> = new List.<String>();
    
    function OnGUI() {
        ReorderableListGUI.ListField(yourList, CustomListItem, DrawEmpty, 0);
    }
    
    function CustomListItem(position:Rect, itemValue:String):String {
        // Text fields do not like null values!
        if (itemValue == null)
            itemValue = '';
        return EditorGUI.TextField(position, itemValue);
    }
    
    function DrawEmpty() {
        GUILayout.Label('No items in list.', EditorStyles.miniLabel);
    }

Submission to the Unity Asset Store
-----------------------------------

If you wish to include this asset as part of a package for the asset store, please
include the latest package version as-is to avoid conflict issues in user projects.
LICENSE and README.md files must be included and remain intact.

If you would like to include a modified version of this project within your asset:

- Ensure that LICENSE and README.md are included and remain intact.
- Copyright and license information must remain intact.
- Change the namespace `Rotorz.ReorderableList` to something unique and DO NOT
  use the name "Rotorz".
- Copy scripts into your own asset folder.

This is to avoid causing conflicts if somebody downloads multiple assets which
make use of this project.

Useful links
------------

- [Rotorz Website](<http://rotorz.com>)

Contribution Agreement
----------------------

This project is licensed under the BSD license (see LICENSE). To be in the best
position to enforce these licenses the copyright status of this project needs to
be as simple as possible. To achieve this the following terms and conditions
must be met:

- All contributed content (including but not limited to source code, text,
  image, videos, bug reports, suggestions, ideas, etc.) must be the
  contributors own work.

- The contributor disclaims all copyright and accepts that their contributed
  content will be released to the [public domain](<http://en.wikipedia.org/wiki/Public_domain>).

- The act of submitting a contribution indicates that the contributor agrees
  with this agreement. This includes (but is not limited to) pull requests, issues,
  tickets, e-mails, newsgroups, blogs, forums, etc.

### Disclaimer

External content linked in the above text are for convienence purposes only and
do not contribute to the agreement in any way. Linked content should be digested
under the readers discretion.
