### 使应用在dock上面没有图标 (xcode 6.1)
	在项目的info里面添加一项叫 Application is agent(UIElement) 设置为 YES

### 使应用没有主窗口 (xcode 6.1)
	在右边打开 Main.storyboard 这个文件,删除里面的所有窗口项.

### 在StatusBar上有图标 (xcode 6.1)
	主要就是 NSStatusItem 这个对象
	在 AppDelegate.h 添加下列内容
```
#import <Cocoa/Cocoa.h>

@interface AppDelegate : NSObject <NSApplicationDelegate>

@property (assign) IBOutlet NSWindow *window;
@property (nonatomic, strong) NSStatusItem* item;

@end
```

	在 AppDelegate.m 里面的 applicationDidFinishLaunching 方法上面添加下列内容
```
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    self.item = [[NSStatusBar systemStatusBar] statusItemWithLength:20];
    NSImage *image = [NSImage imageNamed:@"menu_icon"];
    //[image setTemplate:YES];
    self.item.image = image;
    self.item.highlightMode = YES;

    NSMenu *menu = [[NSMenu alloc] initWithTitle:@"Shadowsocks"];
    [menu setMinimumWidth:200];

    enableMenuItem = [[NSMenuItem alloc] initWithTitle:@"关闭快喵加速器" action:@selector(toggleRunning) keyEquivalent:@""];

    [menu addItem:enableMenuItem];
    [menu addItemWithTitle:@"退出" action:@selector(exit) keyEquivalent:@""];

    self.item.menu = menu;
}
```