## TO REPRO:

Run commands precisely in this order:

```
npm run clean
npm run clean.mobile
npm run start.mobile
```

You will see it prepares `nativescript-ui-core` twice and also installs it's sub node_modules within itself causing the problem. 

Likely the app will crash with the following when it's run:

`Details:  unexpected successful exit code from cancelled command <C0019:'PBXCp TNSListView.framework':P14>`

Solving requires one to open the XCode and remove the duplicate TNSCore.framework which was erroneously added.

**Proposed Solution**: Right now `nativescript-ui-core` is declared in `dependencies` section on all `ui-*` published modules. Instead try declaring it in `devDependencies` or just making it a prerequisite install - that way users will only ever have exactly 1 installed into their project. The ladder is likely the most versatile as it would suffice several npm project setups.