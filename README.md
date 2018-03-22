# QTLearn
For Qt4.8:
1.Use QSettings to write and read registry
	QSetting set(QSettings::NativeFormat, QSettings::SystemScope,QCoreApplication::organizationName(), QCoreApplication::applicationName()); //Windows:HKEY_LOCAL_MACHINE
	QStringList groupList = set.childGroups();
	foreach(QString group, groupList){
		set.beginGroup(group)
		QString software = set.value("InstallLocation").toString();
		if(software.constains("keyword")
			software is the installation path 
		set.endGroup()
	}

2.	
