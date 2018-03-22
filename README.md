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

2.Use QDomDocument to write and read xml file. Should add xml at the .pro file. QDomElement,QDomNode,QDomText, QDomAttr
	QDomDocument xml;
	QDomProcessingInstruction instruction;
	instruction = xml.createProcessingInstruction("xml, "version=\"1.0\" encoding=\"UTF-8\"");
	xml.appendChild(root);
	QDomElement root = xml.createElement("XXX");
	xml.appendChild(root);
	QDomElement e = xml.createElement("XXXX");
	QDomText text = xml.createTestNode("XXXXX");
	e.appendChild(text);
	root.appendChild(e);
	
	QTextStream outstream(&file);
	xml.save(outstream,4);
	file.close();

	//parse xml file
	xml.setContent(&file);
	QDomElement root = xml.documentElement();
	QDomNode node = root.firstChild();

	while(!node.isNULL()){
		if(node.isElement()){
			QDomElement e = node.toElement();
			if(e.tagName() == "XXX")
			{
				QDomNodeList nl = e.childNodes();
				for(int i=0; i<nl.count(); i++){
					QDomNode n = nl.at(i);
					if(n.isElement()))
						n.toElement().text();
				}
			}
		node = node.nextSibling();
	}

3.QDateTime::currentDataTime().toString("yyyy-MM-dd hh:mm:ss")

4.QByteArray text = QByteArray::fromBase64(text.toAsscii());
	QString s = QString(text.data());
	text = s.toAsscii().toBase64();

5.QProcess to invoke other processes
	QString command="XXXX";
	QProcess proc;
	proc.start(command);
	if(proc.waitForStarted()){
		proc.waitForFinished();
		qDebug()<<readAllStandardOutput();
		qDebug()<<readAllStandardError();//Return value type is QByteArray
		proc.close();
	}

	//use cmd to getprocess start
	proc.start("cmd.exe", QStringList<<"/c"<<command);

6.Use QCryptographicHash to digest string, the first parameter type must be QByteArray. digest method include: Md4, Md5, SHA1
	QString digest = QString(QCryptographicHash::hash(/*QByteArray*/tmp, QCryptographicHash::Md5).toHex());

7.When use the windows API, must include header files. If the error like library not found, add #pragma comment(lib, "XXX.lib") 
	The name of lib can be found on MSDN

8.Modal Dialog and Modeless Dialog. method exec() is modal. If modal feature is false, method show() is modalless. Modal Dialog can be used to get value from dialog. We can also use signal and slot to pass value. Or use public function to pass value between father-and-son window. 
