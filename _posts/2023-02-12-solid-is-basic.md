---
layout: post
permalink: "/post/software-engineering/solid-is-basic"
title:  "S.O.L.I.D is Basic"
date:   2023-02-12 07:24:19 +1100
reading_time: 7
---

If you're planning on starting your journey into the art of coding, new to software development, or even a seasoned professional looking for a refresher, then this blog is for you!

Before we get to it, as a software engineer/professional working in the IT industry, we should always ask! 

*Why should I learn this? What is it for? Is it necessary? How can I apply the concept?*

To answer these question, we must first understand what *technical debt* is all about. Technical debt is referred to as *code smells*. It's basically code that could've been written better. In other words, it's simply refers to the additional time and effort that a dev/team needs to spend on a project due to *shortcuts* taken or *subpar\suboptimal* decisions made during the development process.

Making SOLID your foundation will equip you to avoid these kinds of mistakes and will enable you to focus on the quality of your code.

Now let's get to it..

### **Single Responsibility Principle**
#### `Do one thing and do it well`


Now imagine for a second the experience of opening your christmas present that was wrapped on a thick material using a swiss knife. How was it? It's poor right..

The experience you imagined applies to code. If you have something that does something like the swiss knife, chances are you're not going to do them optimally.

If you're planning on writing a method that will do so much, just simply decompose the process and have multiple smaller methods. Remember, there will always come a time where requirement will change. If the time comes, you will have the responsibility on updating the code. On applying this concept, you have the ease of readibility and maintainability.  

Rule of thumb from Robert C. Martin aka uncle bob: *"There should never be more than one reason a class to change."*

`In order for a function to do “one thing” it must be so small that no meaningful function can be extracted from it.  Any function from which another can be extracted clearly does more than “one thing”.`

Let's take a look on how it works.

{% highlight c# %}
class FileSystem
{
    public void ReadFile(string fileName)
    {
        // code to read a file
    }

    public void WriteFile(string fileName, string content)
    {
        // code to write to a file
    }

    public void SendFileToServer(string fileName)
    {
        // code to send file to server
    }
}
{% endhighlight %}
In this code, the *FileSystem* class has three responsibilities: reading files, writing files, and sending files to a server. 
It clearly violates the principle. 

Now let's apply the principle.

{% highlight c# %}
class FileSystem
{
    public string ReadFile(string fileName)
    {
        // code to read a file
        return "";
    }

    public void WriteFile(string fileName, string content)
    {
        // code to write to a file
    }
}

class FileSender
{
    public void SendFileToServer(string fileName)
    {
        // code to send file to server
    }
}
{% endhighlight %}

The responsibilities of reading files, writing files, and sending files to a server are now separated into two separate classes, *FileSystem* and *FileSender*, respectively. 
This makes the code easier to maintain and test, as changes to one responsibility don't affect the other. Additionally, each class now only has one responsibility, which makes the code easier to understand.

Important Note: `Abstraction is the elimination of the irrelevant and the amplification of the essential.`


### **Open-Closed Principle**
#### `Achieve Modularity and Scalability`

Now imagine for a second you have a small fridge that can store 10 drinks. You now have a party and need to store 20 drinks. Do you take the fridge apart and modify it to make it larger? This would involve making changes to the original design and a risk that the fridge may work once it's done. Or do you simply just borrow/purchase a cooler/storage container and add ice?

The principle has three points:
1. A class should be open for extensibility but closed for modification. 
2. You are not allowed to modify a class once it is being used by other clients
3. Change in a class that is being used by others will cause a ripple effect of change. 

This means, you should design your code in a way that allows you to add new functionality without having to change existing code. By applying this concept, it will help you achieve maintainability, flexibility, and reusability in your code. You now have the ease to modify and extend your code over time as new requirement arise, without having to make major changes to existing code. This can save you a lot of time and effort in the long run, and make your code easier for others to understand and work with.

Let's take a look how it works.

{% highlight c# %}
public enum FileType
{
    TextFileType,
    BinaryFileType
}

public class FileSystem
{
    public void ReadFile(string fileName, FileType fileType)
    {
        if (fileType == FileType.Text)
        {
            // code to read a text file
        }
        else if (fileType == FileType.Binary)
        {
            // code to read a binary file
        }
    }

    public void WriteFile(string fileName, string content, FileType fileType)
    {
        if (fileType == FileType.Text)
        {
            // code to write a text file
        }
        else if (fileType == FileType.Binary)
        {
            // code to write a binary file
        }
    }
}
{% endhighlight %}

 the *FileSystem* class has a *ReadFile* method and a *WriteFile* method, both of which take a *FileType* enum parameter that determines the type of file being read or written. This is a violation, as adding a new file type requires modifying the existing code.

 Now let's apply the principle.

{% highlight c# %}
public interface IFile
{
    void Read(string fileName);
    void Write(string fileName, string content);
}

public class TextFile : IFile
{
    public void Read(string fileName)
    {
        // code to read a text file
    }

    public void Write(string fileName, string content)
    {
        // code to write a text file
    }
}

public class BinaryFile : IFile
{
    public void Read(string fileName)
    {
        // code to read a binary file
    }

    public void Write(string fileName, string content)
    {
        // code to write a binary file
    }
}

public class FileSystem
{
    private readonly IFile _file;

    public FileSystem(IFile file)
    {
        _file = file;
    }

    public void ReadFile(string fileName)
    {
        _file.Read(fileName);
    }

    public void WriteFile(string fileName, string content)
    {
        _file.Write(fileName, content);
    }
}
{% endhighlight %}

 The *TextFile* and *BinaryFile* classes both implement the *IFile* interface, which defines the *Read* and *Write* methods. The *FileSystem* class now has a constructor that takes an *IFile* parameter, and it delegates the file operations to the *IFile* implementation. This means that adding a new file type can be done by creating a new class that implements the *IFile* interface, without modifying the existing code. This follows the principle, as the code is closed for modification but open for extension.

Important Note: `Composition should be preferred over inheritance.`

### **Liskov Substitution Principle**
#### `Maximize Software Interoperability`

Now imagine for a second you have a base class that represents a certain type of object, and then you have subclasses that inherit from that base class, each representing a specific variation of that object. The principle says that you should be able to substitute a subclass for the base class, without causing any problems.

In other words, if you have a method that accepts an object of the base class, it should work the same way, regardless of whether you pass in an object of the base class or one of its subclasses. This allows you to make changes to your codebase over time, knowing that you won't break existing functionality.

Let's take a look how it works.

{% highlight c# %}
public class File
{
    public virtual void Open()
    {
        Console.WriteLine("Opening file");
    }
}

public class ImageFile : File
{
    public override void Open()
    {
        Console.WriteLine("Opening image file");
        throw new Exception("Image files cannot be opened");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        File file = new ImageFile();
        file.Open();
    }
}
{% endhighlight %}

 The *File* class has a virtual Open method, and the *ImageFile* class overrides this method and throws an exception when it is called. However, if we have a reference to a *File* object and it is actually an instance of *ImageFile*, then this will cause a runtime exception. This violates the principle because ImageFile is not substitutable for File.

 Now let's apply the principle.

 {% highlight c# %}
public abstract class File
{
    public abstract void Open();
}

public class ImageFile : File
{
    public override void Open()
    {
        Console.WriteLine("Cannot open image file");
    }
}

public class TextFile : File
{
    public override void Open()
    {
        Console.WriteLine("Opening text file");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        File file = new ImageFile();
        file.Open();
        
        file = new TextFile();
        file.Open();
    }
}
 {% endhighlight %}

 The *File* class is now abstract, and the *Open* method is abstract as well.
 The *ImageFile* and *TextFile* classes both inherit from File and provide their own implementations of the Open method. This allows us to have a reference to a File object and know that the Open method is always available, even if the actual instance is an instance of ImageFile.
 This follows the principle because *ImageFile* and *TextFile* are substitutable for *File*.

Important Note: `Subclass objects must behave the same as base class objects.`

### **Interface Segregation Principle**
#### `Keep Interfaces Focused and Specific`

Now imagine you've been tasked with creating a file system. You need to create classes to represent the different types of files, such as audio files, image files, and text files. Each type of file needs to have its own set of actions, such as playing an audio file, viewing an image file, or reading a text file.

Now, let's say you've created an interface called "IFile" that defines all the actions that any file can perform, such as opening, closing, and deleting. But, not all types of files need to perform all these actions. For example, an image file doesn't need to be closed or an audio file doesn't need to be deleted.

This is the principle comes into play. You should create separate interfaces for each specific set of actions that's different types of files need to perform. In this case, you can create an interface for audio files called "IAudioFile", an interface for image files called "IImageFile", and an interface for text files called "ITextFile". Each of these interfaces will only contain the actions that are specific to the type of file they represent.

Let's take a look how it works.

{% highlight c# %}
public interface IFile
{
    void Open();
    void Close();
    void Read();
    void Write();
    void Delete();
}

public class AudioFile : IFile
{
    public void Open()
    {
        Console.WriteLine("Audio file is opened");
    }

    public void Close()
    {
        Console.WriteLine("Audio file is closed");
    }

    public void Read()
    {
        Console.WriteLine("Audio file cannot be read");
    }

    public void Write()
    {
        Console.WriteLine("Audio file cannot be written");
    }

    public void Delete()
    {
        Console.WriteLine("Audio file is deleted");
    }
}

public class ImageFile : IFile
{
    public void Open()
    {
        Console.WriteLine("Image file is opened");
    }

    public void Close()
    {
        Console.WriteLine("Image file cannot be closed");
    }

    public void Read()
    {
        Console.WriteLine("Image file is read");
    }

    public void Write()
    {
        Console.WriteLine("Image file cannot be written");
    }

    public void Delete()
    {
        Console.WriteLine("Image file is deleted");
    }
}
{% endhighlight %}

*AudioFile* and *ImageFile* classes are forced to implement all the methods defined in the *IFile* interface, even if they don't actually use all of them. This leads to a lot of unnecessary code and makes it harder to maintain the file system.

Let's take a look how it works.

{% highlight c# %}
public interface IReadableFile
{
    void Open();
    void Read();
}

public interface IWritableFile
{
    void Write();
    void Delete();
}

public class AudioFile : IReadableFile, IWritableFile
{
    public void Open()
    {
        Console.WriteLine("Audio file is opened");
    }

    public void Read()
    {
        Console.WriteLine("Audio file cannot be read");
    }

    public void Write()
    {
        Console.WriteLine("Audio file cannot be written");
    }

    public void Delete()
    {
        Console.WriteLine("Audio file is deleted");
    }
}

public class ImageFile : IReadableFile, IWritableFile
{
    public void Open()
    {
        Console.WriteLine("Image file is opened");
    }

    public void Read()
    {
        Console.WriteLine("Image file is read");
    }

    public void Write()
    {
        Console.WriteLine("Image file cannot be written");
    }

    public void Delete()
    {
        Console.WriteLine("Image file is deleted");
    }
}
{% endhighlight %}

We now have split the *IFile* interface into two smaller, more specific interfaces: *IReadableFile* and *IWritableFile*. The *AudtioFile* and *ImageFile* classes now only need to implement the methods that they actually need, resulting in a more modular and maintanable file system.

Important Note: `Keep interfaces lean and focused`

### **Dependency Inversion Principle**
#### `Elavate Abstraction for Loose Coupling`

Now imagine for a second you are designing a file system that needs to access various storage devices such as hard drives, flash drives, and cloud storage. In a traditional approach, you might have the file system dependent on concrete storage devices, meaning that if you wanted to add a new storage device, you would have to make changes directly to the file system code.

The principle dictates that you should design the file system to depend on abstractions, such as an interface for storage devices. This way, if you wanted to add a new storage device, you could simply create a new implementation of the storage interface, without having to make any changes to the file system code. 

This helps to decouple the file system code from the concrete storage devices, making it more flexible and scalable in the long run.

Let's take a look how it works.

{% highlight c# %}
public class FileSystem
{
    public void StoreData(HardDrive hardDrive)
    {
        // Code to store data on hard drive
    }

    public void StoreData(FlashDrive flashDrive)
    {
        // Code to store data on flash drive
    }
}

public class HardDrive
{
    // Hard drive implementation
}

public class FlashDrive
{
    // Flash drive implementation
}
{% endhighlight %}

The *FileSystem* class directly creates an instance of the *File* class and calls its methods to perform various file operations.
This voilates the principle because it has a high-level module *FileSystem* that is dependent on a low-level module *File*. This makes the code tightly coupled and harder to maintain and test.

Now let's apply the principle.

{% highlight c# %}
public interface IStorageDevice
{
    void StoreData();
}

public class HardDrive : IStorageDevice
{
    public void StoreData()
    {
        // Code to store data on hard drive
    }
}

public class FlashDrive : IStorageDevice
{
    public void StoreData()
    {
        // Code to store data on flash drive
    }
}

public class FileSystem
{
    private IStorageDevice _storageDevice;

    public FileSystem(IStorageDevice storageDevice)
    {
        _storageDevice = storageDevice;
    }

    public void StoreData()
    {
        _storageDevice.StoreData();
    }
}
{% endhighlight %}

*FileSystem* class depends on the abstract *IStorageDevice* interface, rather than on concrete implementations such as *HardDrive* and *FlashDrive*. This makes it more flexible and scalable, as adding a new storage device simply requires implementing the IStorageDevice interface.

The principle is achieved by inverting the direction of the dependencies, so that high-level components dependend on abstractions, while low-level components depend on concrete implementations.

Important Note: `High-level modules should not depend on low-level modules. Both should depend on abstractions`
