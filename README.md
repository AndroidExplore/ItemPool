# ItemPool
[![Apache 2.0 License](https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=flat)](http://www.apache.org/licenses/LICENSE-2.0.html) [![Release](https://img.shields.io/github/release/nekocode/ItemPool.svg?label=Jitpack)](https://jitpack.io/#nekocode/ItemPool)

Decouple the item(/nested viewholder) from recyclerview's adapter.

![description](art/description.png)

### Using with gradle
- Add the JitPack repository to your project root build.gradle:
```gradle
repositories {
    maven { url "https://jitpack.io" }
}
```

- Add the dependency to your app or lib build.gradle:
```gradle
dependencies {
    compile 'com.github.nekocode:ItemPool:{lastest-version}'
}
```

### Usage

Create reusable items for recyclerview.

```java
public class TestItem extends Item<String> {
    TextView textView;

    @NonNull
    @Override
    public View onCreateItemView(@NonNull LayoutInflater inflater, @NonNull ViewGroup parent) {
        View itemView = inflater.inflate(R.layout.item_test, parent, false);
        textView = (TextView) itemView.findViewById(R.id.textView);
        return itemView;
    }

    @Override
    public void onBindItem(@NonNull final RecyclerView.ViewHolder holder, @NonNull String s, ItemEventHandler eventHandler) {
        textView.setText(s);
    }
}
```

No more need adpater and data list. You just need an `ItemPool`.

Add itemtypes and data to the ItemPool. It will help the recyclerview automatically select the Item to show.

```java
ItemPool items = new ItemPool();
items.addType(TestItem.class);
items.addType(TestItem2.class);

items.add(new TestData2());
items.add(new TestData());
items.add(new TestData2());

items.attachTo(recyclerView);
```

For more detail about handling of the item event, see the [sample here](sample/src/main/java/cn/nekocode/itempool/sample/MainActivity.java).