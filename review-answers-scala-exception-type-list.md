
# Exceptions in Scala
## Notes:
- Scala Throwable extends [java.lang.Throwable](https://docs.oracle.com/javase/8/docs/api/java/lang/Throwable.html#java.lang.Throwable)
- Scala has no checked exceptions ([ref1](https://www.informit.com/articles/article.aspx?p=1849236&seqNum=12#:~:text=However%2C%20unlike%20Java%2C%20Scala%20has,IOException%2C%20you%20must%20declare%20it.))

#### Important methods:
- getMessage() - Returns a detailed message
- getCause() - Returns cause or null if unknown/null
- printStackTrace() - Prints error and backtrace to console
- getStackTrace() - Get stack trace for programatic use

## java.lang.Exception  Subclass List

- [AclNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/security/acl/AclNotFoundException.html "class in java.security.acl")
reference to non-existent ACL (Access Control List)
- [ActivationException](https://docs.oracle.com/javase/8/docs/api/java/rmi/activation/ActivationException.html "class in java.rmi.activation")
general exception used by the activation interfaces
- [AlreadyBoundException](https://docs.oracle.com/javase/8/docs/api/java/rmi/AlreadyBoundException.html "class in java.rmi")
thrown when trying to bind an object in registry that is already bound
- [ApplicationException](https://docs.oracle.com/javase/8/docs/api/org/omg/CORBA/portable/ApplicationException.html "class in org.omg.CORBA.portable")
- [AWTException](https://docs.oracle.com/javase/8/docs/api/java/awt/AWTException.html "class in java.awt")
- [BackingStoreException](https://docs.oracle.com/javase/8/docs/api/java/util/prefs/BackingStoreException.html "class in java.util.prefs")
- [BadAttributeValueExpException](https://docs.oracle.com/javase/8/docs/api/javax/management/BadAttributeValueExpException.html "class in javax.management")
- [BadBinaryOpValueExpException](https://docs.oracle.com/javase/8/docs/api/javax/management/BadBinaryOpValueExpException.html "class in javax.management")
- [BadLocationException](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/BadLocationException.html "class in javax.swing.text")
- [BadStringOperationException](https://docs.oracle.com/javase/8/docs/api/javax/management/BadStringOperationException.html "class in javax.management")
- [BrokenBarrierException](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BrokenBarrierException.html "class in java.util.concurrent")
- [CertificateException](https://docs.oracle.com/javase/8/docs/api/javax/security/cert/CertificateException.html "class in javax.security.cert")
- [CloneNotSupportedException](https://docs.oracle.com/javase/8/docs/api/java/lang/CloneNotSupportedException.html "class in java.lang")
- [DataFormatException](https://docs.oracle.com/javase/8/docs/api/java/util/zip/DataFormatException.html "class in java.util.zip")
- [DatatypeConfigurationException](https://docs.oracle.com/javase/8/docs/api/javax/xml/datatype/DatatypeConfigurationException.html "class in javax.xml.datatype")
- [DestroyFailedException](https://docs.oracle.com/javase/8/docs/api/javax/security/auth/DestroyFailedException.html "class in javax.security.auth")
- [ExecutionException](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutionException.html "class in java.util.concurrent")
- [ExpandVetoException](https://docs.oracle.com/javase/8/docs/api/javax/swing/tree/ExpandVetoException.html "class in javax.swing.tree")
- [FontFormatException](https://docs.oracle.com/javase/8/docs/api/java/awt/FontFormatException.html "class in java.awt")
- [GeneralSecurityException](https://docs.oracle.com/javase/8/docs/api/java/security/GeneralSecurityException.html "class in java.security")
- [GSSException](https://docs.oracle.com/javase/8/docs/api/org/ietf/jgss/GSSException.html "class in org.ietf.jgss")
- [IllegalClassFormatException](https://docs.oracle.com/javase/8/docs/api/java/lang/instrument/IllegalClassFormatException.html "class in java.lang.instrument")
- [InterruptedException](https://docs.oracle.com/javase/8/docs/api/java/lang/InterruptedException.html "class in java.lang")
- [IntrospectionException](https://docs.oracle.com/javase/8/docs/api/java/beans/IntrospectionException.html "class in java.beans")
- [InvalidApplicationException](https://docs.oracle.com/javase/8/docs/api/javax/management/InvalidApplicationException.html "class in javax.management")
- [InvalidMidiDataException](https://docs.oracle.com/javase/8/docs/api/javax/sound/midi/InvalidMidiDataException.html "class in javax.sound.midi")
- [InvalidPreferencesFormatException](https://docs.oracle.com/javase/8/docs/api/java/util/prefs/InvalidPreferencesFormatException.html "class in java.util.prefs")
- [InvalidTargetObjectTypeException](https://docs.oracle.com/javase/8/docs/api/javax/management/modelmbean/InvalidTargetObjectTypeException.html "class in javax.management.modelmbean")
- [IOException](https://docs.oracle.com/javase/8/docs/api/java/io/IOException.html "class in java.io")
- [JAXBException](https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/JAXBException.html "class in javax.xml.bind")
- [JMException](https://docs.oracle.com/javase/8/docs/api/javax/management/JMException.html "class in javax.management")
- [KeySelectorException](https://docs.oracle.com/javase/8/docs/api/javax/xml/crypto/KeySelectorException.html "class in javax.xml.crypto")
- [LambdaConversionException](https://docs.oracle.com/javase/8/docs/api/java/lang/invoke/LambdaConversionException.html "class in java.lang.invoke")
- [LastOwnerException](https://docs.oracle.com/javase/8/docs/api/java/security/acl/LastOwnerException.html "class in java.security.acl")
- [LineUnavailableException](https://docs.oracle.com/javase/8/docs/api/javax/sound/sampled/LineUnavailableException.html "class in javax.sound.sampled")
- [MarshalException](https://docs.oracle.com/javase/8/docs/api/javax/xml/crypto/MarshalException.html "class in javax.xml.crypto")
- [MidiUnavailableException](https://docs.oracle.com/javase/8/docs/api/javax/sound/midi/MidiUnavailableException.html "class in javax.sound.midi")
- [MimeTypeParseException](https://docs.oracle.com/javase/8/docs/api/java/awt/datatransfer/MimeTypeParseException.html "class in java.awt.datatransfer")
- [MimeTypeParseException](https://docs.oracle.com/javase/8/docs/api/javax/activation/MimeTypeParseException.html "class in javax.activation")
- [NamingException](https://docs.oracle.com/javase/8/docs/api/javax/naming/NamingException.html "class in javax.naming")
- [NoninvertibleTransformException](https://docs.oracle.com/javase/8/docs/api/java/awt/geom/NoninvertibleTransformException.html "class in java.awt.geom")
- [NotBoundException](https://docs.oracle.com/javase/8/docs/api/java/rmi/NotBoundException.html "class in java.rmi")
- [NotOwnerException](https://docs.oracle.com/javase/8/docs/api/java/security/acl/NotOwnerException.html "class in java.security.acl")
- [ParseException](https://docs.oracle.com/javase/8/docs/api/java/text/ParseException.html "class in java.text")
- [ParserConfigurationException](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/ParserConfigurationException.html "class in javax.xml.parsers")
- [PrinterException](https://docs.oracle.com/javase/8/docs/api/java/awt/print/PrinterException.html "class in java.awt.print")
- [PrintException](https://docs.oracle.com/javase/8/docs/api/javax/print/PrintException.html "class in javax.print")
- [PrivilegedActionException](https://docs.oracle.com/javase/8/docs/api/java/security/PrivilegedActionException.html "class in java.security")
- [PropertyVetoException](https://docs.oracle.com/javase/8/docs/api/java/beans/PropertyVetoException.html "class in java.beans")
- [ReflectiveOperationException](https://docs.oracle.com/javase/8/docs/api/java/lang/ReflectiveOperationException.html "class in java.lang")
- [RefreshFailedException](https://docs.oracle.com/javase/8/docs/api/javax/security/auth/RefreshFailedException.html "class in javax.security.auth")
- [RemarshalException](https://docs.oracle.com/javase/8/docs/api/org/omg/CORBA/portable/RemarshalException.html "class in org.omg.CORBA.portable")
- [RuntimeException](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html "class in java.lang")
- [SAXException](https://docs.oracle.com/javase/8/docs/api/org/xml/sax/SAXException.html "class in org.xml.sax")
- [ScriptException](https://docs.oracle.com/javase/8/docs/api/javax/script/ScriptException.html "class in javax.script")
- [ServerNotActiveException](https://docs.oracle.com/javase/8/docs/api/java/rmi/server/ServerNotActiveException.html "class in java.rmi.server")
- [SOAPException](https://docs.oracle.com/javase/8/docs/api/javax/xml/soap/SOAPException.html "class in javax.xml.soap")
- [SQLException](https://docs.oracle.com/javase/8/docs/api/java/sql/SQLException.html "class in java.sql")
- [TimeoutException](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeoutException.html "class in java.util.concurrent")
- [TooManyListenersException](https://docs.oracle.com/javase/8/docs/api/java/util/TooManyListenersException.html "class in java.util")
- [TransformerException](https://docs.oracle.com/javase/8/docs/api/javax/xml/transform/TransformerException.html "class in javax.xml.transform")
- [TransformException](https://docs.oracle.com/javase/8/docs/api/javax/xml/crypto/dsig/TransformException.html "class in javax.xml.crypto.dsig")
- [UnmodifiableClassException](https://docs.oracle.com/javase/8/docs/api/java/lang/instrument/UnmodifiableClassException.html "class in java.lang.instrument")
- [UnsupportedAudioFileException](https://docs.oracle.com/javase/8/docs/api/javax/sound/sampled/UnsupportedAudioFileException.html "class in javax.sound.sampled")
- [UnsupportedCallbackException](https://docs.oracle.com/javase/8/docs/api/javax/security/auth/callback/UnsupportedCallbackException.html "class in javax.security.auth.callback")
- [UnsupportedFlavorException](https://docs.oracle.com/javase/8/docs/api/java/awt/datatransfer/UnsupportedFlavorException.html "class in java.awt.datatransfer")
- [UnsupportedLookAndFeelException](https://docs.oracle.com/javase/8/docs/api/javax/swing/UnsupportedLookAndFeelException.html "class in javax.swing")
- [URIReferenceException](https://docs.oracle.com/javase/8/docs/api/javax/xml/crypto/URIReferenceException.html "class in javax.xml.crypto")
- [URISyntaxException](https://docs.oracle.com/javase/8/docs/api/java/net/URISyntaxException.html "class in java.net")
- [UserException](https://docs.oracle.com/javase/8/docs/api/org/omg/CORBA/UserException.html "class in org.omg.CORBA")
- [XAException](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAException.html "class in javax.transaction.xa")
- [XMLParseException](https://docs.oracle.com/javase/8/docs/api/javax/management/modelmbean/XMLParseException.html "class in javax.management.modelmbean")
- [XMLSignatureException](https://docs.oracle.com/javase/8/docs/api/javax/xml/crypto/dsig/XMLSignatureException.html "class in javax.xml.crypto.dsig")
- [XMLStreamException](https://docs.oracle.com/javase/8/docs/api/javax/xml/stream/XMLStreamException.html "class in javax.xml.stream")
- [XPathException](https://docs.oracle.com/javase/8/docs/api/javax/xml/xpath/XPathException.html "class in javax.xml.xpath")

## java.lang.RuntimeException Subclass List

- [AnnotationTypeMismatchException](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/AnnotationTypeMismatchException.html "class in java.lang.annotation")
- [ArithmeticException](https://docs.oracle.com/javase/8/docs/api/java/lang/ArithmeticException.html "class in java.lang")
- [ArrayStoreException](https://docs.oracle.com/javase/8/docs/api/java/lang/ArrayStoreException.html "class in java.lang")
- [BufferOverflowException](https://docs.oracle.com/javase/8/docs/api/java/nio/BufferOverflowException.html "class in java.nio")
- [BufferUnderflowException](https://docs.oracle.com/javase/8/docs/api/java/nio/BufferUnderflowException.html "class in java.nio")
- [CannotRedoException](https://docs.oracle.com/javase/8/docs/api/javax/swing/undo/CannotRedoException.html "class in javax.swing.undo")
- [CannotUndoException](https://docs.oracle.com/javase/8/docs/api/javax/swing/undo/CannotUndoException.html "class in javax.swing.undo")
- [ClassCastException](https://docs.oracle.com/javase/8/docs/api/java/lang/ClassCastException.html "class in java.lang")
- [CMMException](https://docs.oracle.com/javase/8/docs/api/java/awt/color/CMMException.html "class in java.awt.color")
- [CompletionException](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletionException.html "class in java.util.concurrent")
- [ConcurrentModificationException](https://docs.oracle.com/javase/8/docs/api/java/util/ConcurrentModificationException.html "class in java.util")
- [DataBindingException](https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/DataBindingException.html "class in javax.xml.bind")
- [DateTimeException](https://docs.oracle.com/javase/8/docs/api/java/time/DateTimeException.html "class in java.time")
- [DOMException](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/DOMException.html "class in org.w3c.dom")
- [EmptyStackException](https://docs.oracle.com/javase/8/docs/api/java/util/EmptyStackException.html "class in java.util")
- [EnumConstantNotPresentException](https://docs.oracle.com/javase/8/docs/api/java/lang/EnumConstantNotPresentException.html "class in java.lang")
- [EventException](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/events/EventException.html "class in org.w3c.dom.events")
- [FileSystemAlreadyExistsException](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemAlreadyExistsException.html "class in java.nio.file")
- [FileSystemNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemNotFoundException.html "class in java.nio.file")
- [IllegalArgumentException](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html "class in java.lang")
- [IllegalMonitorStateException](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalMonitorStateException.html "class in java.lang")
- [IllegalPathStateException](https://docs.oracle.com/javase/8/docs/api/java/awt/geom/IllegalPathStateException.html "class in java.awt.geom")
- [IllegalStateException](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalStateException.html "class in java.lang")
- [IllformedLocaleException](https://docs.oracle.com/javase/8/docs/api/java/util/IllformedLocaleException.html "class in java.util")
- [ImagingOpException](https://docs.oracle.com/javase/8/docs/api/java/awt/image/ImagingOpException.html "class in java.awt.image")
- [IncompleteAnnotationException](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/IncompleteAnnotationException.html "class in java.lang.annotation")
- [IndexOutOfBoundsException](https://docs.oracle.com/javase/8/docs/api/java/lang/IndexOutOfBoundsException.html "class in java.lang")
- [JMRuntimeException](https://docs.oracle.com/javase/8/docs/api/javax/management/JMRuntimeException.html "class in javax.management")
- [LSException](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/ls/LSException.html "class in org.w3c.dom.ls")
- [MalformedParameterizedTypeException](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/MalformedParameterizedTypeException.html "class in java.lang.reflect")
- [MalformedParametersException](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/MalformedParametersException.html "class in java.lang.reflect")
- [MirroredTypesException](https://docs.oracle.com/javase/8/docs/api/javax/lang/model/type/MirroredTypesException.html "class in javax.lang.model.type")
- [MissingResourceException](https://docs.oracle.com/javase/8/docs/api/java/util/MissingResourceException.html "class in java.util")
- [NegativeArraySizeException](https://docs.oracle.com/javase/8/docs/api/java/lang/NegativeArraySizeException.html "class in java.lang")
- [NoSuchElementException](https://docs.oracle.com/javase/8/docs/api/java/util/NoSuchElementException.html "class in java.util")
- [NoSuchMechanismException](https://docs.oracle.com/javase/8/docs/api/javax/xml/crypto/NoSuchMechanismException.html "class in javax.xml.crypto")
- [NullPointerException](https://docs.oracle.com/javase/8/docs/api/java/lang/NullPointerException.html "class in java.lang")
- [ProfileDataException](https://docs.oracle.com/javase/8/docs/api/java/awt/color/ProfileDataException.html "class in java.awt.color")
- [ProviderException](https://docs.oracle.com/javase/8/docs/api/java/security/ProviderException.html "class in java.security")
- [ProviderNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/nio/file/ProviderNotFoundException.html "class in java.nio.file")
- [RasterFormatException](https://docs.oracle.com/javase/8/docs/api/java/awt/image/RasterFormatException.html "class in java.awt.image")
- [RejectedExecutionException](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RejectedExecutionException.html "class in java.util.concurrent")
- [SecurityException](https://docs.oracle.com/javase/8/docs/api/java/lang/SecurityException.html "class in java.lang")
- [SystemException](https://docs.oracle.com/javase/8/docs/api/org/omg/CORBA/SystemException.html "class in org.omg.CORBA")
- [TypeConstraintException](https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/TypeConstraintException.html "class in javax.xml.bind")
- [TypeNotPresentException](https://docs.oracle.com/javase/8/docs/api/java/lang/TypeNotPresentException.html "class in java.lang")
- [UncheckedIOException](https://docs.oracle.com/javase/8/docs/api/java/io/UncheckedIOException.html "class in java.io")
- [UndeclaredThrowableException](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/UndeclaredThrowableException.html "class in java.lang.reflect")
- [UnknownEntityException](https://docs.oracle.com/javase/8/docs/api/javax/lang/model/UnknownEntityException.html "class in javax.lang.model")
- [UnmodifiableSetException](https://docs.oracle.com/javase/8/docs/api/javax/print/attribute/UnmodifiableSetException.html "class in javax.print.attribute")
- [UnsupportedOperationException](https://docs.oracle.com/javase/8/docs/api/java/lang/UnsupportedOperationException.html "class in java.lang")
- [WebServiceException](https://docs.oracle.com/javase/8/docs/api/javax/xml/ws/WebServiceException.html "class in javax.xml.ws")
- [WrongMethodTypeException](https://docs.oracle.com/javase/8/docs/api/java/lang/invoke/WrongMethodTypeException.html "class in java.lang.invoke")

## java.io.IOException

Thrown...

- [ChangedCharSetException](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/ChangedCharSetException.html "class in javax.swing.text")
...when charset is changed
- [CharacterCodingException](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/CharacterCodingException.html "class in java.nio.charset")
...on character encoding or decoding error
- [CharConversionException](https://docs.oracle.com/javase/8/docs/api/java/io/CharConversionException.html "class in java.io")
base class for character conversion expcetions
- [ClosedChannelException](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/ClosedChannelException.html "class in java.nio.channels")
...when attempt to operate on channel closed to that operation
- [EOFException](https://docs.oracle.com/javase/8/docs/api/java/io/EOFException.html "class in java.io")
...to signal EOF or end of stream reached unexpectedly
- [FileLockInterruptionException](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/FileLockInterruptionException.html "class in java.nio.channels")
...when another thread interrupts a file lock request
- [FileNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/io/FileNotFoundException.html "class in java.io")
...thrown when file doesn't exist or cant be accessed
- [FilerException](https://docs.oracle.com/javase/8/docs/api/javax/annotation/processing/FilerException.html "class in javax.annotation.processing")
...on errors involving Filer guarantees
- [FileSystemException](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystemException.html "class in java.nio.file")
general class for file system exceptions.
- [HttpRetryException](https://docs.oracle.com/javase/8/docs/api/java/net/HttpRetryException.html "class in java.net")
...to indicate HTTP request not possible
- [IIOException](https://docs.oracle.com/javase/8/docs/api/javax/imageio/IIOException.html "class in javax.imageio")
...to signal run-time failure of r/w operations
- [InterruptedByTimeoutException](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/InterruptedByTimeoutException.html "class in java.nio.channels")
checked exception when async operation timeouts
- [InterruptedIOException](https://docs.oracle.com/javase/8/docs/api/java/io/InterruptedIOException.html "class in java.io")
...to signal I/O operation has been interrupted
- [InvalidPropertiesFormatException](https://docs.oracle.com/javase/8/docs/api/java/util/InvalidPropertiesFormatException.html "class in java.util")
...to indicate oper could not complete because property format error
- [JMXProviderException](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXProviderException.html "class in javax.management.remote")
...jmx error
- [JMXServerErrorException](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXServerErrorException.html "class in javax.management.remote")
...jmx error
- [MalformedURLException](https://docs.oracle.com/javase/8/docs/api/java/net/MalformedURLException.html "class in java.net")

- [ObjectStreamException](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectStreamException.html "class in java.io")

- [ProtocolException](https://docs.oracle.com/javase/8/docs/api/java/net/ProtocolException.html "class in java.net")

- [RemoteException](https://docs.oracle.com/javase/8/docs/api/java/rmi/RemoteException.html "class in java.rmi")

- [SaslException](https://docs.oracle.com/javase/8/docs/api/javax/security/sasl/SaslException.html "class in javax.security.sasl")

- [SocketException](https://docs.oracle.com/javase/8/docs/api/java/net/SocketException.html "class in java.net")

- [SSLException](https://docs.oracle.com/javase/8/docs/api/javax/net/ssl/SSLException.html "class in javax.net.ssl")

- [SyncFailedException](https://docs.oracle.com/javase/8/docs/api/java/io/SyncFailedException.html "class in java.io")

- [UnknownHostException](https://docs.oracle.com/javase/8/docs/api/java/net/UnknownHostException.html "class in java.net")

- [UnknownServiceException](https://docs.oracle.com/javase/8/docs/api/java/net/UnknownServiceException.html "class in java.net")

- [UnsupportedDataTypeException](https://docs.oracle.com/javase/8/docs/api/javax/activation/UnsupportedDataTypeException.html "class in javax.activation")

- [UnsupportedEncodingException](https://docs.oracle.com/javase/8/docs/api/java/io/UnsupportedEncodingException.html "class in java.io")

- [UserPrincipalNotFoundException](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/UserPrincipalNotFoundException.html "class in java.nio.file.attribute")

- [UTFDataFormatException](https://docs.oracle.com/javase/8/docs/api/java/io/UTFDataFormatException.html "class in java.io")

- [ZipException](https://docs.oracle.com/javase/8/docs/api/java/util/zip/ZipException.html "class in java.util.zip")


## java.lang.Error Subclass List

- [AnnotationFormatError](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/AnnotationFormatError.html "class in java.lang.annotation")
- [AssertionError](https://docs.oracle.com/javase/8/docs/api/java/lang/AssertionError.html "class in java.lang")
- [AWTError](https://docs.oracle.com/javase/8/docs/api/java/awt/AWTError.html "class in java.awt")
- [CoderMalfunctionError](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/CoderMalfunctionError.html "class in java.nio.charset")
- [FactoryConfigurationError](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/FactoryConfigurationError.html "class in javax.xml.parsers")
- [FactoryConfigurationError](https://docs.oracle.com/javase/8/docs/api/javax/xml/stream/FactoryConfigurationError.html "class in javax.xml.stream")
- [IOError](https://docs.oracle.com/javase/8/docs/api/java/io/IOError.html "class in java.io")
- [LinkageError](https://docs.oracle.com/javase/8/docs/api/java/lang/LinkageError.html "class in java.lang")
- [SchemaFactoryConfigurationError](https://docs.oracle.com/javase/8/docs/api/javax/xml/validation/SchemaFactoryConfigurationError.html "class in javax.xml.validation")
- [ServiceConfigurationError](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceConfigurationError.html "class in java.util")
- [ThreadDeath](https://docs.oracle.com/javase/8/docs/api/java/lang/ThreadDeath.html "class in java.lang")
- [TransformerFactoryConfigurationError](https://docs.oracle.com/javase/8/docs/api/javax/xml/transform/TransformerFactoryConfigurationError.html "class in javax.xml.transform")
- [VirtualMachineError](https://docs.oracle.com/javase/8/docs/api/java/lang/VirtualMachineError.html "class in java.lang")
