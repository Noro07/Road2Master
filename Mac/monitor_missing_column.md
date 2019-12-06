# Activity Monitor Columns Are Missing

解决方法，删除掉会自动生成新的就可以了

Let us first state the obvious. As you probably know, you can add or remove columns by choosing View > Columns from the menu bar. Are columns selected? If not, select them and this will fix the issue

## Still, columns are missing? We will delete the Activity Monitor app preferences. Here is how:

1. First, quit the Activity Monitor app if it is running
2. Go to the Finder of Mac OS
3. Click the Go menu
4. Click the Go To Folder menu (shurtcut: Command+Shift+G)Go To Folder
5. This will open a window. In this window, enter the following command and click Go.
6. ~/Library/Preferences/com.apple.ActivityMonitor.plistActivity Monitor Preferences
7. This will open the Preferences window with com.apple.ActivityMonitor.plist selected.com.apple.ActivityMonitor.plist
8. Delete this file by moving it to the Trash
9. Now open Activity Monitor and check if columns are there.

ref: <https://macreports.com/activity-monitor-columns-are-missing-fix/>
