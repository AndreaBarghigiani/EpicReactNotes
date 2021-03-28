> Code for this function is kept in [this repo](https://github.com/AndreaBarghigiani/utility-fns/tree/main/objects/valueFromPath)

The reason that I started dig into [[Recursion]] is because I needed to get all the values inside an object. Lets say for example that I have this kind of object:
```js
const obj = {
  dismiss: {
    feature_popup: {
      custom_labels: "dismiss_feature_popup_custom_labels",
      website_switcher: "dismiss_feature_popup_website_switcher",
      expand_view: "dismiss_feature_popup_expand_view"
    },

    hideOverviewHostingMigrationCard: "hideOverviewHostingMigrationCard",
    new_dot: "dismiss_new_dot" // Old feature badge but still
  },
  language: "language",
  uptime_interval: "uptime_interval",
  whatsnew_last_seen: "whatsnew_last_seen",
  default_user_role: "default_user_role",
  renderWS: "renderWS",
  show_expanded_update_list: "show_expanded_update_list"
};
```
What I want to get from `allValues` is this kind of array that lists all the values in the object, even in the nested ones:
```js
const AllValues = allValues(obj);
console.log(AllValues)

// Will print
[
	"dismiss_feature_popup_custom_labels",
	"dismiss_feature_popup_website_switcher",
	"dismiss_feature_popup_expand_view"
	"hideOverviewHostingMigrationCard",
	"dismiss_new_dot",
	"language",
	"uptime_interval",
	"whatsnew_last_seen",
	"default_user_role",
	"renderWS",
	"show_expanded_update_list",
];
```
The function I came up with is:
```js
function allValues(obj) {
	let allVals = [];
	
	for (let key of Object.keys(obj)) {
		typeof obj[key] === "object"
			? allVals.push(...allValues(obj[key]))
			: allVals.push(obj[key]);
	}
  
	return allVals;
}
```