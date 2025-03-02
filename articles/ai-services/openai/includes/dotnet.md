---
title: 'Quickstart: Use Azure OpenAI Service with the C# SDK'
titleSuffix: Azure OpenAI
description: Walkthrough on how to get started with Azure OpenAI and make your first completions call with the C# SDK. 
services: cognitive-services
manager: nitinme
ms.service: cognitive-services
ms.subservice: openai
ms.topic: include
author: mrbullwinkle
ms.author: mbullwin
ms.date: 07/26/2023
keywords: 
---

[Source code](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/openai/Azure.AI.OpenAI/src) | [Package (NuGet)](https://www.nuget.org/packages/Azure.AI.OpenAI/) | [Samples](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/openai/Azure.AI.OpenAI/tests/Samples)

## Prerequisites

- An Azure subscription - [Create one for free](https://azure.microsoft.com/free/cognitive-services?azure-portal=true)
- Access granted to the Azure OpenAI service in the desired Azure subscription.
    Currently, access to this service is granted only by application. You can apply for access to Azure OpenAI Service by completing the form at [https://aka.ms/oai/access](https://aka.ms/oai/access?azure-portal=true).
- The current version of <a href="https://dotnet.microsoft.com/download/dotnet-core" target="_blank">.NET Core</a>
- An Azure OpenAI Service resource with the `text-davinci-003` model deployed. For more information about model deployment, see the [resource deployment guide](../how-to/create-resource.md).

> [!div class="nextstepaction"]
> [I ran into an issue with the prerequisites.](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=DOTNET&Pillar=AOAI&Product=gpt&Page=quickstart&Section=Prerequisites)

## Set up

### Create a new .NET Core application

In a console window (such as cmd, PowerShell, or Bash), use the `dotnet new` command to create a new console app with the name `azure-openai-quickstart`. This command creates a simple "Hello World" project with a single C# source file: *Program.cs*.

```dotnetcli
dotnet new console -n azure-openai-quickstart
```

Change your directory to the newly created app folder. You can build the application with:

```dotnetcli
dotnet build
```

The build output should contain no warnings or errors.

```output
...
Build succeeded.
 0 Warning(s)
 0 Error(s)
...
```

Install the OpenAI .NET client library with:

```console
dotnet add package Azure.AI.OpenAI --prerelease
```

[!INCLUDE [get-key-endpoint](get-key-endpoint.md)]

[!INCLUDE [environment-variables](environment-variables.md)]


> [!div class="nextstepaction"]
> [I ran into an issue with the setup.](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=DOTNET&Pillar=AOAI&Product=gpt&Page=quickstart&Section=Set-up)

## Create .NET application

From the project directory, open the *program.cs* file and replace with the following code:

```csharp
using Azure;
using Azure.AI.OpenAI;
using static System.Environment;

string endpoint = GetEnvironmentVariable("AZURE_OPENAI_ENDPOINT");
string key = GetEnvironmentVariable("AZURE_OPENAI_KEY");

// Enter the deployment name you chose when you deployed the model.
string engine = "text-davinci-003";

OpenAIClient client = new(new Uri(endpoint), new AzureKeyCredential(key));

string prompt = "When was Microsoft founded?";
Console.Write($"Input: {prompt}\n");

Response<Completions> completionsResponse = 
    await client.GetCompletionsAsync(engine, prompt);
string completion = completionsResponse.Value.Choices[0].Text;
Console.WriteLine($"Chatbot: {completion}");
```

> [!IMPORTANT]
> For production, use a secure way of storing and accessing your credentials like [Azure Key Vault](../../../key-vault/general/overview.md). For more information about credential security, see the Azure AI services [security](../../security-features.md) article.

```cmd
dotnet run program.cs
```

## Output

```console
Input: When was Microsoft founded?
Chatbot:

Microsoft was founded on April 4, 1975
```

> [!div class="nextstepaction"]
> [I ran into an issue when running the code sample.](https://microsoft.qualtrics.com/jfe/form/SV_0Cl5zkG3CnDjq6O?PLanguage=DOTNET&Pillar=AOAI&Product=gpt&Page=quickstart&Section=Create-dotnet-application)


## Clean up resources

If you want to clean up and remove an OpenAI resource, you can delete the resource. Before deleting the resource you must first delete any deployed models.

- [Portal](../../multi-service-resource.md?pivots=azportal#clean-up-resources)
- [Azure CLI](../../multi-service-resource.md?pivots=azcli#clean-up-resources)

## Next steps

* For more examples check out the [Azure OpenAI Samples GitHub repository](https://aka.ms/AOAICodeSamples)
