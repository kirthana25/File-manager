package org.jext.dawn.io;
import java.io.*;
import org.jext.dawn.*;
public class FileManager
{
 public static final String NEW_LINE = System.getProperty("line.separator")
 public static void openFileForInput(StringID,String file,Function function,DawnParser parser)
 {
  if(!isFileAvailable(ID,parser))
  {
   try
   {
     parser.setProperty("DAWN.IO#FILE."+ID,new BufferReader(new FileReader( 
                         DawnUtilities.constructPath(file))));
     }catch (IDException ioe) { 
     throw new DawnRuntimeException(function,parser,"file" +file+ "not found"}
     }
    }else
    throw new DawmnRunTime Exception(function,parser,"file ID " + ID+ " already exists");
    }
    public static String readLine(String ID, Function function , DawnParser parser) throws DawnRuntimeException
    {
    return read(true, ID, function, parser);
    }
    Public static String read(String ID, Function function, DawnParser parser) throws DawnRuntimeException
    { 
     return read(false , ID, function, parser);
     }
     public static String read(boolean line, String ID, Function function, DawnParser parser) throws DawnRuntimeException
     {
       Object obj= parser.getProperty("DAWN.IO#FILE."+ ID);
       if (!(obj instanceceof BufferedReader))
          throw new DawnRuntimeException(function, parser, "attempted to read from an output file");
       BufferedReader in = (BufferdReader) obj;
       if(in != null)
       {
        try
        {
         if (line)
         {
         String_line = in.readLine();
         if (_line == null)
              closeFile(ID, function, parser);
            else
              return_line;
          } else {
            char c= (char) in.read();
            if (c == '\0')
              closeFile(ID, function,parser);
            else
              return new StringBuffer().append(c).toString();
              }
              catch(IOException ioe) {
              throw  new DawnRuntimeException(function,parser, "file ID"+ ID + " cannot be written properly");
              }
              }else
               throw new DawnRuntimeException(function, parser,"file ID" +ID + " points to a non-opened file");
               }
               public static void closeFile(String ID, Function function, Dawnparser parser) throws DawntimeException
               {
                object obj = parser.gerproperty("DAWN.IO#FILE." + ID);
                if(obj == null)
                 return;
                
                if(!(obj instanceof Reader) && !(obj instanceof Writer)
                   throw new DawnRuntimeException(function, parser,"error, given ID" + ID + "does not point to a file");
                   try
                   {
                    if (obj instanceof Reader)
                       ((BufferedReader) obj).close();
                    else
                      { 
                        BufferdWriter out = (BufferedWriter) obj;
                        out.flush();
                        out.close();
                        }
                    parser.unsetProperty("DAWN.IO#FILE."+ID);
                    }catch(IOException ioe) {
                    throw new DawnRuntimeException(function.parser,"cannot close file ID" + ID);
                    }
                   }
                   public static boolean isFileAvailable(String ID,DawnParser parser)
                   {
                    return (parser.getProperty("DAWN.IO#FILE." + ID) != null);
                    }
                   }
                        
       
          
        
  
    
