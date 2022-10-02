Fork of https://github.com/kimxogus/react-native-version-check which does not require expo-localization, and instead accepts a country parameter.

Usage:

```
import VersionCheck from 'expo-react-native-version-checker';

import * as React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import VersionCheck from 'expo-react-native-version-check'
import Constants from 'expo-constants';
import * as appjson from './app.json';



// or any pure javascript modules available in npm
import { Card } from 'react-native-paper';

export default function App() {
  const [currentVersion, setCurrentVersion] = React.useState(null);
  const [isUpdateNeeded, setIsUpdateNeeded] = React.useState(false)
  
  React.useEffect(()=>{
    setCurrentVersion(VersionCheck('HU').getCurrentVersion());
  }, [])
  

  React.useEffect(()=>{
    if(currentVersion){
      VersionCheck('HU').needUpdate({
        currentVersion: currentVersion,
        latestVersion: "52.0.0"
      }).then(res => {
        setIsUpdateNeeded(JSON.stringify(res.isNeeded));
      });
    }
  }, [currentVersion])
  
  return (
    <View style={styles.container}>
      <Card>
        <Text>
          CV: {currentVersion}
        </Text>
        <Text>
          UPDATE NEED: {isUpdateNeeded}
        </Text>
        <Text>
          CONSANTS MANIFEST: {Constants.manifest.version} 
        </Text>
        <Text>
          APP JSON {appjson.expo.version}
        </Text>
      </Card>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    paddingTop: Constants.statusBarHeight,
    backgroundColor: '#ecf0f1',
    padding: 8,
  },
  paragraph: {
    margin: 24,
    fontSize: 18,
    fontWeight: 'bold',
    textAlign: 'center',
  },
});

```
