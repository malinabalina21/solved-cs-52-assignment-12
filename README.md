Download Link: https://assignmentchef.com/product/solved-cs-52-assignment-12
<br>
<strong>Directions:</strong>Please complete the following assignment to signify your completion of Unit 17.  All programming projects need to be completed and submitted electronically, following the Electronic Submission Guidelines discussed in class.  Please cherry-pick from your solution folder and submit just the .cpp and .h  files you created or modified as well as .exe file that Visual Studio built from your code.

<strong>Background:</strong>This assignment deals with inheritance.  Inheritance is one of the major principles of object-oriented programming.  In C++, one of the biggest goals is “code reuse”.  Inheritance accomplishes this.  In order to get inheritance working in C++, you must get both the structure of your .h files as well as the implementation of your constructor correct.  Constructor implementations must use an initialization list.  Please review the book and the online content on these issues so you know how it works before you begin..

<h3><strong>part_a: flashdrive 4.0 (inheritance)</strong></h3>

The purpose of this assignment is to work with exceptions and inheritance.  As you may recall, I have provided you with a sample class named FlashDrive which has been diagrammed below.  You will reuse code from previous assignments and further extend it.  I’d like you to enhance this class so that invoking its methods or operators potentially throw a custom exception, rather than just a <tt>std::logic_error</tt>.  As you may recall, you can create a <tt>logic_error</tt> by passing a string value to its constructor.  Officially, you should also say <tt>#include &lt;stdexcept&gt; </tt>to begin working with logic_error, but Visual Studio (being a badly behaved child…) let’s you get away with it.

For this assignment, you will want to focus on subclassing std::logic_error.  In each exceptional situation, rather than writing errors to cout or throwing std::logic_error, please create and throw a custom subclass as shown below:

<table border="1" width="100%" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td width="41%"><img decoding="async" width="240" height="120" name="Graphic1" align="bottom" border="0" data-recalc-dims="1" data-src="https://i0.wp.com/www.howardstahl.com/cs52/logicerror.jpg?resize=240%2C120" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

    <noscript>

     <img decoding="async" src="https://i0.wp.com/www.howardstahl.com/cs52/logicerror.jpg?resize=240%2C120" width="240" height="120" name="Graphic1" align="bottom" border="0" data-recalc-dims="1">

    </noscript></td>

   <td width="59%"><img decoding="async" width="500" height="250" name="Graphic2" align="bottom" border="0" data-recalc-dims="1" data-src="https://i0.wp.com/www.howardstahl.com/cs52/driveexceptions.jpg?resize=500%2C250" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

    <noscript>

     <img decoding="async" src="https://i0.wp.com/www.howardstahl.com/cs52/driveexceptions.jpg?resize=500%2C250" width="500" height="250" name="Graphic2" align="bottom" border="0" data-recalc-dims="1">

    </noscript></td>

  </tr>

 </tbody>

</table>

Please remember that subclasses really MUST call their parent class constructors by using an initialization list.

<table border="1" width="98%" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td width="38%" height="400">

    <table border="1" width="98%" cellspacing="0" cellpadding="0">

     <tbody>

      <tr>

       <td width="100%"><p align="center"><strong>FlashDrive</strong></td>

      </tr>

      <tr>

       <td width="100%">FlashDrive( );FlashDrive( int capacity, int used, bool pluggedIn ); void plugIn( );void pullOut( );void writeData( int amount );void eraseData( int amount );void formatDrive( ); int getCapacity( );void setCapacity( int amount ); int getUsed( );void setUsed( int amount ); bool isPluggedIn( );</td>

      </tr>

      <tr>

       <td width="100%">int my_StorageCapacity;int my_StorageUsed;bool my_IsPluggedIn;</td>

      </tr>

     </tbody>

    </table></td>

   <td width="105%" height="400">

    <table border="1" width="121%" cellspacing="0" cellpadding="0">

     <tbody>

      <tr>

       <td width="100%"><p align="center"><strong>Sample Driver Code</strong></td>

      </tr>

      <tr>

       <td width="100%">FlashDrive empty;FlashDrive drive1( 10, 0, false );FlashDrive drive2( 20, 0, false );FlashDrive * nullPointer = NULL;FlashDrive * pointer = new FlashDrive( 10, 0, false );drive1.plugIn( );drive1.formatDrive( );drive1.writeData( 5 );drive1.pullOut( );cout &lt;&lt; drive1 &lt;&lt; endl;drive2.plugIn( );drive2.formatDrive( );drive2.writeData( 1 );drive2.pullOut( );cout &lt;&lt; drive2 &lt;&lt; endl;FlashDrive combined = drive1 + drive2;cout &lt;&lt; “this drive’s filled to ” &lt;&lt; combined.getUsed( )&lt;&lt; endl;cout &lt;&lt; combined &lt;&lt; endl;FlashDrive other = combined – drive1;cout &lt;&lt; “the other cup’s filled to ” &lt;&lt; other.getUsed( )&lt;&lt; endl;cout &lt;&lt; other &lt;&lt; endl;if (combined &gt; other) {cout &lt;&lt; “looks like combined is bigger…” &lt;&lt; endl;}else {cout &lt;&lt; “looks like other is bigger…” &lt;&lt; endl;}if (drive2 &gt; other) {cout &lt;&lt; “looks like drive2 is bigger…” &lt;&lt; endl;}else {cout &lt;&lt; “looks like other is bigger…” &lt;&lt; endl;}if (drive2 &lt; drive1) {cout &lt;&lt; “looks like drive2 is smaller…” &lt;&lt; endl;}else {cout &lt;&lt; “looks like drive1 is smaller…” &lt;&lt; endl;}// let’s throw some exceptions…try {empty = empty – combined;cout &lt;&lt; “something not right here…” &lt;&lt; endl;} catch( UnderflowingFlashDriveException ) {// an exception should get thrown…// so the lines of code here should// be run, not the cout statement…}try {drive2.writeData( 10000 );cout &lt;&lt; “something not right here…” &lt;&lt; endl;} catch( OverflowingFlashDriveException ) {// an exception should get thrown…// so the lines of code here should// be run, not the cout statement…}try {FlashDrive f( -1, -1, false );cout &lt;&lt; “something not right here…” &lt;&lt; endl;} catch( UnderflowingFlashDriveException ) {// an exception should get thrown…// so the lines of code here should// be run, not the cout statement…}// let’s work with pointers…cout &lt;&lt; nullPointer &lt;&lt; endl; // be careful…cout &lt;&lt; pointer &lt;&lt; endl;cin &gt;&gt; pointer;cout &lt;&lt; pointer; // did the values change?cin &gt;&gt; drive1;cout &lt;&lt; drive1 &lt;&lt; endl; </td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>




<table border="1" width="29%" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td width="15%"><img decoding="async" width="105" height="72" border="0" data-recalc-dims="1" data-src="https://i0.wp.com/www.howardstahl.com/cs52/flash1.jpg?resize=105%2C72" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

    <noscript>

     <img decoding="async" src="https://i0.wp.com/www.howardstahl.com/cs52/flash1.jpg?resize=105%2C72" width="105" height="72" border="0" data-recalc-dims="1">

    </noscript></td>

   <td width="11%"><img decoding="async" width="87" height="100" border="0" data-recalc-dims="1" data-src="https://i0.wp.com/www.howardstahl.com/cs52/flash2.jpg?resize=87%2C100" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

    <noscript>

     <img decoding="async" src="https://i0.wp.com/www.howardstahl.com/cs52/flash2.jpg?resize=87%2C100" width="87" height="100" border="0" data-recalc-dims="1">

    </noscript></td>

  </tr>

 </tbody>

</table>

<h3><strong>part_b: Gambler</strong></h3>

I’d like you to make two inherited gambler classes as described below.  A Gambler is a casino player.  A SlotPlayer is a kind of Gambler who plays casino slot machines.  The relationship between these two classes is shown in the diagram shown below.

<table border="1" width="17%" cellspacing="0" cellpadding="0">

 <tbody>

  <tr>

   <td width="50%"><img decoding="async" width="140" height="115" name="Graphic5" align="bottom" border="0" data-recalc-dims="1" data-src="https://i0.wp.com/www.howardstahl.com/cs52/gamblerHierarchy.jpg?resize=140%2C115" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

    <noscript>

     <img decoding="async" src="https://i0.wp.com/www.howardstahl.com/cs52/gamblerHierarchy.jpg?resize=140%2C115" width="140" height="115" name="Graphic5" align="bottom" border="0" data-recalc-dims="1">

    </noscript></td>

  </tr>

 </tbody>

</table>

Please remember that subclasses really MUST call their parent class constructors by using an initialization list.

<table border="2" width="87%" rules="cols" cellspacing="0" cellpadding="2">

 <colgroup>

  <col width="117">

  <col width="6">

  <col width="133">

 </colgroup>

 <tbody>

  <tr>

   <td width="46%"><p align="center"><strong>Gambler</strong></td>

   <td rowspan="11" valign="top" width="2%"></td>

   <td width="52%"><p align="center"><strong>Driver Code</strong></td>

  </tr>

  <tr>

   <td width="46%">Gambler( std::string name );virtual void win( );virtual void lose( );</td>

   <td rowspan="3" width="52%">Gambler g( “Tom” );SlotPlayer sp( “Tom’s Mother” );g.win( );sp.lose( );g.lose( );sp.win( );</td>

  </tr>

  <tr>

   <td width="46%">std::string myName; // protected</td>

  </tr>

  <tr>

   <td rowspan="2" width="46%"></td>

  </tr>

  <tr>

   <td rowspan="2" width="52%"></td>

  </tr>

  <tr>

   <td rowspan="2" width="46%"><p align="center"><strong>SlotPlayer</strong></td>

  </tr>

  <tr>

   <td rowspan="2" width="52%"><p align="center"><strong>Sample Output</strong></td>

  </tr>

  <tr>

   <td rowspan="2" width="46%">SlotPlayer( std::string name );virtual void win( );virtual void lose( );</td>

  </tr>

  <tr>

   <td rowspan="2" width="52%">The Great Gambler Tom wins!The SlotPlayer Tom’s Mother loses  &#x1f641;The Great Gambler Tom loses!The SlotPlayer Tom’s Mother wins  &#x1f642;</td>

  </tr>

  <tr>

   <td rowspan="2" width="46%"></td>

  </tr>

  <tr>

   <td rowspan="2" width="52%"></td>

  </tr>

  <tr>

   <td colspan="2" width="48%"></td>

  </tr>

 </tbody>

</table>




<ul>

 <li>Your submission should follow this organization, all of which have been provided:

  <ul>

   <li>part_a

    <ul>

     <li>main.cpp</li>

     <li>flashdrive_4_0.h</li>

     <li>flashdrive_4_0.cpp</li>

    </ul></li>

   <li>part_b

    <ul>

     <li>Gambler.cpp</li>

     <li>Gambler.h</li>

     <li>SlotPlayer.cpp</li>

     <li>SlotPlayer.h</li>

     <li>main.cpp</li>

    </ul></li>

  </ul></li>

</ul>