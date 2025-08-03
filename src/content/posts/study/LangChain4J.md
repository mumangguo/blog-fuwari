---
title: LangChain4J的学习笔记
published: 2025-08-03
description: "LangChain4J的学习笔记，记录了我在学习LangChain4J过程中遇到的问题和解决方案。"
image: "./cover.jpg"
tags: ["LangChain4J"]
category: 学习笔记
draft: false
---

# LangChain4J

LangChain4j 的目标是简化将 LLM 集成到 Java 应用程序中的过程。

官网：https://docs.langchain4j.info/

大语言模型排行榜：https://superclueai.com/

支持的模型：https://docs.langchain4j.info/integrations/language-models/

# 入门

官方文档：https://docs.langchain4j.info/get-started

1.创建Maven管理的Java项目并添加LangChain4J依赖

```xml
<!--引入junit依赖，用于单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
<!--引入langchain4j依赖-->
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai</artifactId>
    <version>1.0.0-beta3</version>
</dependency>
```

2.创建测试类

```java
import dev.langchain4j.model.openai.OpenAiChatModel;

import org.junit.jupiter.api.Test;

public class TestLangChain4j {

    @Test
    public void testLangChain4j() {
        OpenAiChatModel model = OpenAiChatModel.builder()
                .baseUrl("http://langchain4j.dev/demo/openai/v1")
                .apiKey("demo")
                .modelName("gpt-4o-mini")
                .build();
        String msg = model.chat("你好");
        System.out.println(msg);
    }
}
```

# SpringBoot集成

## Demo

官方文档：https://docs.langchain4j.info/tutorials/spring-boot-integration

1.创建SpringBoot项目并添加LangChain4J-Starter依赖

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai-spring-boot-starter</artifactId>
    <version>1.0.0-beta3</version>
</dependency>
```

2.修改application.properties配置文件

```properties
# langchain4j配置
# 如果apikey=demo,则baseurl必须为http://langchain4j.dev/demo/openai/v1. if ("demo".equals(builder.apiKey) && !"http://langchain4j.dev/demo/openai/v1".equals(builder.baseUrl))
langchain4j.open-ai.chat-model.base-url=http://langchain4j.dev/demo/openai/v1
langchain4j.open-ai.chat-model.api-key=demo
langchain4j.open-ai.chat-model.model-name=gpt-4o
langchain4j.open-ai.chat-model.log-requests=true
langchain4j.open-ai.chat-model.log-responses=true
```

3.创建测试类

```java
import dev.langchain4j.model.chat.ChatLanguageModel;
import dev.langchain4j.model.openai.OpenAiChatModel;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestLangChain4j {

    @Resource
    private OpenAiChatModel openAiChatModel;
    // 注入这个也可以
    // private ChatLanguageModel model;

    @Test
    public void testLangChain4j2() {
        String msg = openAiChatModel.chat("你是谁");
        System.out.println(msg);
    }
}
```



## DeepSeek

1.访问DeepSeek官方注册账号实名认证后获取API-KEY，官网：https://www.deepseek.com/，点击右上角的API 开放平台 ↗完成注册、实名认证并充值1-10元的余额即可开始使用！

2.创建SpringBoot项目并添加LangChain4J-Starter依赖

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai-spring-boot-starter</artifactId>
    <version>1.0.0-beta3</version>
</dependency>
```

3.修改application.properties配置文件

通过https://platform.deepseek.com/api_keys创建API keys并将API keys保存到系统的环境变量中，避免API keys泄露！**在配置完成后需要重启代码编辑器才能获取到！**

```properties
# langchain4j配置
langchain4j.open-ai.chat-model.base-url=https://api.deepseek.com
# 读取系统环境变量中配置的DEEP_LAKE_API_KEY
langchain4j.open-ai.chat-model.api-key=${DEEP_SEEK_API_KEY}
#langchain4j.open-ai.chat-model.model-name=deepseek-chat
langchain4j.open-ai.chat-model.model-name=deepseek-reasoner
langchain4j.open-ai.chat-model.log-requests=true
langchain4j.open-ai.chat-model.log-responses=true
```

4.创建测试类

```java
import dev.langchain4j.model.chat.ChatLanguageModel;
import dev.langchain4j.model.openai.OpenAiChatModel;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestLangChain4j {

    @Resource
    private OpenAiChatModel openAiChatModel;
    // 注入这个也可以
    // private ChatLanguageModel model;

    @Test
    public void testLangChain4j2() {
        String msg = openAiChatModel.chat("你是谁");
        System.out.println(msg);
    }
}
```



## Ollama

Ollama是一个先进的人工智能工具，允许用户在本地（在CPU和GPU模式下）轻松设置和运行大型语言模型。有了Ollama，用户可以利用强大的语言模型，比如Llama 2，甚至可以定制和创建他们自己的模型。Ollama将模型权重、配置和数据捆绑到一个由Modelfile定义的包中。它优化设置和配置细节，包括GPU使用。

官方文档：https://docs.langchain4j.info/integrations/language-models/ollama#get-started

1.参考文档：https://blog.csdn.net/m0_63823719/article/details/144937845完成Ollama本地大模型的部署

2.创建SpringBoot项目并添加Ollama-LangChain4J-Starter依赖

```xml
		<!-- 引入langchain4j-ollama依赖 -->
        <dependency>
            <groupId>dev.langchain4j</groupId>
            <artifactId>langchain4j-ollama-spring-boot-starter</artifactId>
        </dependency>
```

3.修改application.properties配置文件

```properties
# ollama配置
# ollama的base-url,默认http://localhost:11434
langchain4j.ollama.chat-model.base-url=http://localhost:11434
# 指定模型名称
langchain4j.ollama.chat-model.model-name=llama3-cn
# 开启请求日志,默认false
langchain4j.ollama.chat-model.log-requests=true
# ollama的请求超时时间,60秒
langchain4j.ollama.chat-model.timeout=PT60S
```

4.创建测试类

```java
import dev.langchain4j.model.ollama.OllamaChatModel;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestLangChain4j {

    @Resource
    private OllamaChatModel ollamaChatModel;

    @Test
    public void testOllama() {
        String msg = ollamaChatModel.chat("你是谁");
        System.out.println(msg);
    }
}
```



## 阿里云百炼平台

阿里云百炼是2023年10月推出的。它集成了阿里的通义系列大模型和第三方大模型，涵盖文本、图像、音视频等不同模态。

功能优势：集成超百款大模型API，模型选择丰富；5-10分钟就能低代码快速构建智能体，应用构建高效；提供全链路模型训练、评估工具及全套应用开
发工具，模型服务多元；在线部署可按需扩缩容，新用户有千万token免费送，业务落地成本低。

官方网站：https://bailian.console.aliyun.com/#/home

支持接入的模型列表：https://help.aliyun.com/zh/model-studio/models

模型广场：https://bailian.console.aliyun.com/?productCode=p_efm#/model-market

开通百炼大模型服务并创建apikey：https://bailian.console.aliyun.com/?tab=app#/api-key，并将apikey配置到系统环境变量中避免apikey泄露！**在配置完成后需要重启代码编辑器才能获取到！**

参考文档：https://docs.langchain4j.info/integrations/language-models/dashscope#spring-boot

### 通义千问-文本生成模型

1.创建SpringBoot项目并添加依赖

```xml
<!-- 引入阿里云百炼平台所需的依赖 -->
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-community-dashscope-spring-boot-starter</artifactId>
    <version>1.0.0-alpha1</version>
</dependency>
```

2.修改application.properties配置文件

```properties
# 阿里云百炼平台配置
# 读取系统环境变量中配置的ALIYUN_PLATFORM_API_KEY
langchain4j.community.dashscope.chat-model.api-key=${ALIYUN_PLATFORM_API_KEY}
# 指定模型名称
langchain4j.community.dashscope.chat-model.model-name=qwen-max
```

3.创建测试类

```java
package com.mmg;

import dev.langchain4j.community.model.dashscope.QwenChatModel;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestLangChain4j {

    @Resource
    private QwenChatModel qwenChatModel;

    @Test
    public void testQwen() {
        String msg = qwenChatModel.chat("你是谁");
        System.out.println(msg);
    }
}
```

### 通义万相-图片生成模型

步骤同上，创建测试类进行测试

```java
import dev.langchain4j.community.model.dashscope.WanxImageModel;
import dev.langchain4j.data.image.Image;
import dev.langchain4j.model.output.Response;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.net.URI;

@SpringBootTest
public class TestLangChain4j {

    @Test
    public void testWanxImage() {
        WanxImageModel wanxImageModel = WanxImageModel.builder()
                .modelName("wanx2.1-t2i-plus")
                .apiKey(System.getenv("ALIYUN_PLATFORM_API_KEY"))
                .build();
        Response<Image> response = wanxImageModel.generate("蒸汽朋克城市：巨大的齿轮和管道纵横交错，覆盖着整个城市的建筑。高耸入云的烟囱中喷出浓浓的黑烟，天空被染成了暗灰色。街道上，蒸汽驱动的机械车辆穿梭往来，发出嘈杂的轰鸣声。人们穿着皮质的长风衣、戴着护目镜和金属头盔，手中拿着各种机械工具和武器。一座巨大的钟楼矗立在城市中央，齿轮在钟楼上飞速转动，钟声沉闷而悠远。城市边缘，巨大的蒸汽动力飞行器缓缓升空，准备开始新的旅程。");
        URI url = response.content().url();
        System.out.println(url);
    }
}
```

### 接入DeepSeek

1.创建SpringBoot项目并添加依赖

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai-spring-boot-starter</artifactId>
    <version>1.0.0-beta3</version>
</dependency>
```

2.修改application.properties配置文件

参考文档：https://bailian.console.aliyun.com/?productCode=p_efm&tab=api#/api/?type=model&url=https%3A%2F%2Fhelp.aliyun.com%2Fdocument_detail%2F2868565.html

```properties
# 配置baseurl
langchain4j.open-ai.chat-model.base-url=https://dashscope.aliyuncs.com/compatible-mode/v1
# 读取系统环境变量中配置的ALIYUN_PLATFORM_API_KEY
langchain4j.open-ai.chat-model.api-key=${ALIYUN_PLATFORM_API_KEY}
langchain4j.open-ai.chat-model.model-name=deepseek-r1
langchain4j.open-ai.chat-model.log-requests=true
langchain4j.open-ai.chat-model.log-responses=true
```

3.创建测试类

```java
import dev.langchain4j.model.openai.OpenAiChatModel;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestLangChain4j {

    @Resource
    private OpenAiChatModel openAiChatModel;
    // 注入这个也可以
    // private ChatLanguageModel model;

    @Test
    public void testDashScopeDeepSeek() {
        String msg = openAiChatModel.chat("你是谁");
        System.out.println(msg);
    }
}
```



# AIService

## 介绍

AIService使用面向接口和动态代理的方式完成程序的编写，更灵活的实现高级功能。

在LangChain4j中我们使用AIService完成复杂操作。底层组件将由AIService进行组装。

AlService可处理最常见的操作：

- 为大语言模型格式化输入内容
- 解析大语言模型的输出结果

它们还支持更高级的功能：

- 聊天记忆 Chat memory
- 工具 Tools
- 检索增强生成 RAG

官方文档：https://docs.langchain4j.info/tutorials/ai-services

## 入门

1.创建SpringBoot项目并添加依赖

```xml
        <!-- 引入阿里云百炼平台所需的依赖 -->
        <dependency>
            <groupId>dev.langchain4j</groupId>
            <artifactId>langchain4j-community-dashscope-spring-boot-starter</artifactId>
        </dependency>
		<!-- langchain4j高级功能所需的依赖 -->
        <dependency>
            <groupId>dev.langchain4j</groupId>
            <artifactId>langchain4j-spring-boot-starter</artifactId>
            <version>1.0.0-beta3</version>
        </dependency>
```

2.修改application.properties配置文件

```properties
# 阿里云百炼平台配置
# 读取系统环境变量中配置的ALIYUN_PLATFORM_API_KEY
langchain4j.community.dashscope.chat-model.api-key=${ALIYUN_PLATFORM_API_KEY}
# 指定模型名称
langchain4j.community.dashscope.chat-model.model-name=qwen-max
```

3.创建Assistant接口

```java
package com.mmg.assistant;

public interface Assistant {
    String chat(String userMessage);
}
```

4.创建测试类

```java
import com.mmg.assistant.Assistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.service.AiServices;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestAIService {

    @Resource
    private QwenChatModel qwenChatModel;

    @Test
    public void testQwen() {
        Assistant assistant = AiServices.create(Assistant.class, qwenChatModel);
        String msg = assistant.chat("你是谁");
        System.out.println(msg);
    }
}
```

5.使用注解的方式完成，修改Assistant接口，添加@AiService注解

```java
package com.mmg.assistant;

import dev.langchain4j.service.spring.AiService;

import static dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT;

//@AiService //添加@AiService注解，将Assistant注入到Spring容器中
// 当有多个模型时，需要将wiringMode改为EXPLICIT以及使用chatModel指定使用的模型，否则会报错：
// Conflict: multiple beans of type dev.langchain4j.model.chat.ChatLanguageModel are found: [qwenChatModel, ollamaChatModel, openAiChatModel]. Please specify which one you wish to wire in the @AiService annotation like this: @AiService(wiringMode = EXPLICIT, chatModel = "<beanName>").
@AiService(wiringMode = EXPLICIT, chatModel = "qwenChatModel")
public interface Assistant {
    String chat(String userMessage);
}
```

6.创建测试类

```java
package com.mmg;

import com.mmg.assistant.Assistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.service.AiServices;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class TestAIService {

    @Resource
    private QwenChatModel qwenChatModel;

    @Resource
    private Assistant assistant;

    @Test
    public void testQwen() {
        Assistant assistant = AiServices.create(Assistant.class, qwenChatModel);
        String msg = assistant.chat("你是谁");
        System.out.println(msg);
    }

    @Test
    public void testQwen2() {
        String msg = assistant.chat("你是谁");
        System.out.println(msg);
    }

}
```

AiServices工作原理

AiServices会组装Assistant接口以及其他组件，并使用反射机制创建一个实现Assistant接口的代理对象。这个代理对象会处理输入和输出的所有转换工作。在这个例子中，chat方法的输入是一个字符串，但是大模型需要一个UserMessage对象。所以，代理对象将这个字符串转换为UserMessage，并调用聊天语言模型。chat方法的输出类型也是字符串，但是大模型返回的是AiMessage对象，代理对象会将其转换为字符串。
简单理解就是：代理对象的作用是输入转换和输出转换



# 聊天记忆

## 入门

1.测试对话是否有记忆，目前的接入方式是无法实现聊天记忆的！

```java
import com.mmg.assistant.Assistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class ChatMemoryTest {

    @Resource
    private Assistant assistant;

    @Test
    public void test1() {
        // 你好！很高兴认识你，木芒果。这个名字听起来很有趣也很有特色。请问有什么我可以帮助你的吗？或者你想聊些什么呢？
        String msg = assistant.chat("我是木芒果");
        System.out.println(msg);

        // 您好！您是使用这个平台的用户。不过，您的问题似乎是在寻求更个人化的答案。在这样的对话中，我无法直接知道您的名字或身份信息，因为我是致力于保护用户隐私的。如果您是想告诉我更多关于您自己的信息，或者有其他想要讨论的话题，请随时告诉我！
        String msg2 = assistant.chat("我是谁");
        System.out.println(msg2);
    }
}
```

2.简单实现聊天记忆

```java
import com.mmg.assistant.Assistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.data.message.AiMessage;
import dev.langchain4j.data.message.UserMessage;
import dev.langchain4j.model.chat.response.ChatResponse;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.util.Arrays;

@SpringBootTest
public class ChatMemoryTest {

    @Resource
    private QwenChatModel qwenChatModel;

    @Test
    public void test2() {
        // 第一轮对话
        UserMessage userMessage1 = UserMessage.userMessage("我是木芒果");
        ChatResponse chatResponse1 = qwenChatModel.chat(userMessage1);
        AiMessage aiMessage1 = chatResponse1.aiMessage();
        String msg = aiMessage1.text();
        System.out.println(msg);

        // 第二轮对话
        UserMessage userMessage2 = UserMessage.userMessage("我是谁");
        ChatResponse chatResponse2 = qwenChatModel.chat(Arrays.asList(userMessage1, aiMessage1, userMessage2));
        AiMessage aiMessage2 = chatResponse2.aiMessage();
        String msg2 = aiMessage2.text();
        System.out.println(msg2);
    }
}
```

## 使用ChatMemory

1.简单实现

```java
import com.mmg.assistant.Assistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.data.message.AiMessage;
import dev.langchain4j.data.message.UserMessage;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import dev.langchain4j.model.chat.response.ChatResponse;
import dev.langchain4j.service.AiServices;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class ChatMemoryTest {

    @Resource
    private QwenChatModel qwenChatModel;

    @Test
    public void test3() {
        MessageWindowChatMemory chatMemory = MessageWindowChatMemory.withMaxMessages(10);

        Assistant assistant = AiServices.builder(Assistant.class)
                .chatLanguageModel(qwenChatModel)
                .chatMemory(chatMemory)
                .build();
        // 第一轮对话 你好！很高兴认识你，木芒果。这个名字听起来很有趣也很有特色。请问有什么我可以帮助你的吗？或者你想聊些什么话题呢？
        String msg = assistant.chat("我是木芒果");
        System.out.println(msg);

        // 第二轮对话 你刚刚告诉我，你是木芒果。如果你是在用这个名字或昵称来介绍自己，那么你就是木芒果。如果你有其他身份或想进一步澄清，可以告诉我更多信息哦！
        String msg2 = assistant.chat("我是谁");
        System.out.println(msg2);
    }
}
```

2.使用注解的方式，创建MemoryChatAssistant接口，加上@AiService注解，在注解中指定chatMemory

```java
package com.mmg.assistant;

import dev.langchain4j.service.spring.AiService;

import static dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT;


@AiService(wiringMode = EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemory = "chatMemory")
public interface MemoryChatAssistant {
    String chat(String userMessage);
}
```

3.创建chatMemory配置类

```java
package com.mmg.config;

import dev.langchain4j.memory.ChatMemory;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MemoryChatAssistantConfig {

    @Bean
    public ChatMemory chatMemory() {
        return MessageWindowChatMemory.withMaxMessages(10);
    }
}
```

4.创建测试类

```java
import com.mmg.assistant.Assistant;
import com.mmg.assistant.MemoryChatAssistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.data.message.AiMessage;
import dev.langchain4j.data.message.UserMessage;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import dev.langchain4j.model.chat.response.ChatResponse;
import dev.langchain4j.service.AiServices;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class ChatMemoryTest {

    @Resource
    private MemoryChatAssistant memoryChatAssistant;

    @Test
    public void test4() {
        String msg = memoryChatAssistant.chat("我是木芒果");
        System.out.println(msg);

        String msg2 = memoryChatAssistant.chat("我是谁");
        System.out.println(msg2);
    }
}
```



## 隔离聊天记忆

为每个用户的新聊天或者不同的用户区分聊天记忆

1.创建隔离聊天记忆接口，通过指定chatMemoryProvider实现聊天记忆隔离

```java
import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider") //通过指定chatMemoryProvider实现聊天记忆隔离
public interface SeparateChatAssistant {

    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```

2.创建隔离聊天记忆配置类

```java
import dev.langchain4j.memory.chat.ChatMemoryProvider;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import dev.langchain4j.store.memory.chat.InMemoryChatMemoryStore;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SeparateChatAssistantConfig {

    @Bean
    public ChatMemoryProvider chatMemoryProvider() {
        return memoryId -> MessageWindowChatMemory.builder()
                .id(memoryId)
                .maxMessages(10)
                // 默认使用的是SingleSlotChatMemoryStore,改为内存存储
                .chatMemoryStore(new InMemoryChatMemoryStore())
                .build();
    }
}
```

3.创建测试类

```java
import com.mmg.assistant.Assistant;
import com.mmg.assistant.MemoryChatAssistant;
import com.mmg.assistant.SeparateChatAssistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.data.message.AiMessage;
import dev.langchain4j.data.message.UserMessage;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import dev.langchain4j.model.chat.response.ChatResponse;
import dev.langchain4j.service.AiServices;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class ChatMemoryTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void test5() {
        /**
         * 你好！很高兴认识你，木芒果。这个名字听起来很有趣也很有特色。有什么我可以帮助你的吗？或者你想聊些什么呢？
         * 你刚刚告诉我，你是木芒果。如果你是在以“木芒果”作为你的昵称或代号，那么我就可以称呼你为木芒果。如果你有其他想要了解的身份信息或者有其他问题需要解答，请告诉我！
         *
         * 你好，张三！很高兴见到你。有什么我可以帮助你的吗？如果你有任何问题或需要什么信息，请随时告诉我。
         * 你刚才告诉我你是张三。如果你是在开玩笑或者有其他意思，请告诉我，我很乐意继续我们的对话！
         */
        String msg = separateChatAssistant.chat(1, "我是木芒果");
        System.out.println(msg);
        String msg2 = separateChatAssistant.chat(1, "我是谁");
        System.out.println(msg2);

        String msg3 = separateChatAssistant.chat(2, "我是张三");
        System.out.println(msg3);
        String msg4 = separateChatAssistant.chat(2, "我是谁");
        System.out.println(msg4);
    }
}
```



## 持久化聊天记忆

默认情况下，聊天记忆存储在内存中。如果需要持久化存储，可以实现一个自定义的聊天记忆存储类，以便将聊天消息存储在你选择的任何持久化存储介质
中。

MySQL

- 特点：关系型数据库。支持事务处理，确保数据的一致性和完整性，适用于结构化数据的存储和查询。

- 适用场景：如果聊天记忆数据结构较为规整，例如包含固定的字段如对话ID、用户ID、时间戳、消息内容等，且需要进行复杂的查询和统计分析，如按用户统计对话次数、按时间范围查询特定对话等，MySQL是不错的选择。

Redis

- 特点：内存数据库，读写速度极高。它适用于存储热点数据，并且支持多种数据结构，如字符串、哈希表、列表等，方便对不同类型的聊天记忆数据进行处理。
- 适用场景：对于实时性要求极高的聊天应用，如在线客服系统或即时通讯工具，Redis可以快速存储和获取最新的聊天记录，以提供流畅的聊天体验。

MongoDB

- 特点：文档型数据库，数据以JSON-like的文档形式存储，具有高度的灵活性和可扩展性。它不需要预先定义严格的表结构，适合存储半结构化或非结构化的数据。
- 适用场景：当聊天记忆中包含多样化的信息，如文本消息、图片、语音等多媒体数据，或者消息格式可能会频繁变化时，MongoDB能很好地适应这种灵活性。例如，一些社交应用中用户可能会发送各种格式的消息，使用MongoDB可以方便地存储和管理这些不同类型的数据。

Cassandra

- 特点：是一种分布式的NOSQL数据库，具有高可扩展性和高可用性，能够处理大规模的分布式数据存储和读写请求。适合存储海量的、时间序列相关的数据。
- 适用场景：对于大型的聊天应用，尤其是用户量众多、聊天数据量巨大且需要分布式存储和处理的场景，Cassandra能够有效地应对高并发的读写操作。例如，一些面向全球用户的社交媒体平台，其聊天数据需要在多个节点上进行分布式存储和管理，Cassandra可以提供强大的支持。

安装MongoDB

下载链接：https://www.mongodb.com/download-center/community

详细安装教程：https://blog.csdn.net/weixin_42039228/article/details/123657641

1.引入spring-boot-starter-data-mongodb起步依赖

```xml
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-mongodb</artifactId>
        </dependency>
```

2.添加mongo连接配置

```properties
# 配置mongodb
spring.data.mongodb.uri=mongodb://localhost:27017/chat_history
```

3.创建ChatMessages实体映射类

```java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import org.bson.types.ObjectId;
import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Document("chat_messages")
public class ChatMessages {

    @Id // 唯一标识，映射到MongoDB的_id字段,使用ObjectId类型
    private ObjectId messageId;

    private String memoryId;

    // 存储聊天消息的内容
    private String content;
}
```

4.创建自定义消息存储类,通过实现ChatMemoryStore接口

```java
import com.mmg.bean.ChatMessages;
import dev.langchain4j.data.message.ChatMessage;
import dev.langchain4j.data.message.ChatMessageDeserializer;
import dev.langchain4j.data.message.ChatMessageSerializer;
import dev.langchain4j.store.memory.chat.ChatMemoryStore;
import jakarta.annotation.Resource;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.query.Criteria;
import org.springframework.data.mongodb.core.query.Query;
import org.springframework.data.mongodb.core.query.Update;
import org.springframework.stereotype.Repository;

import java.util.LinkedList;
import java.util.List;

@Repository
public class MongoChatMemoryStore implements ChatMemoryStore {

    @Resource
    private MongoTemplate mongoTemplate;

    @Override
    public List<ChatMessage> getMessages(Object memoryId) {
        Criteria criteria = Criteria.where("memoryId").is(memoryId);
        Query query = new Query(criteria);
        ChatMessages chatMessages = mongoTemplate.findOne(query, ChatMessages.class);
        if (chatMessages == null) {
            return new LinkedList<>();
        }
        String contentJson = chatMessages.getContent();
        return ChatMessageDeserializer.messagesFromJson(contentJson);
    }

    @Override
    public void updateMessages(Object memoryId, List<ChatMessage> list) {
        Criteria criteria = Criteria.where("memoryId").is(memoryId);
        Query query = new Query(criteria);
        Update update = new Update();
        update.set("content", ChatMessageSerializer.messagesToJson(list));
        mongoTemplate.upsert(query, update, ChatMessages.class);
    }

    @Override
    public void deleteMessages(Object memoryId) {
        Criteria criteria = Criteria.where("memoryId").is(memoryId);
        Query query = new Query(criteria);
        mongoTemplate.remove(query, ChatMessages.class);
    }
}
```

5.创建隔离聊天记忆接口

```java
import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider") //通过指定chatMemoryProvider实现聊天记忆隔离
public interface SeparateChatAssistant {

    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```

6.创建隔离聊天记忆配置类，并使用mongodb存储消息

```java
package com.mmg.config;

import com.mmg.store.MongoChatMemoryStore;
import dev.langchain4j.memory.chat.ChatMemoryProvider;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import jakarta.annotation.Resource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SeparateChatAssistantConfig {

    @Resource
    private MongoChatMemoryStore mongoChatMemoryStore;

    @Bean
    public ChatMemoryProvider chatMemoryProvider() {
        return memoryId -> MessageWindowChatMemory.builder()
                .id(memoryId)
                .maxMessages(10)
                // 使用MongoDB作为存储
                .chatMemoryStore(mongoChatMemoryStore)
                .build();
    }
}
```

7.创建测试类

```java
import com.mmg.assistant.Assistant;
import com.mmg.assistant.MemoryChatAssistant;
import com.mmg.assistant.SeparateChatAssistant;
import dev.langchain4j.community.model.dashscope.QwenChatModel;
import dev.langchain4j.data.message.AiMessage;
import dev.langchain4j.data.message.UserMessage;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import dev.langchain4j.model.chat.response.ChatResponse;
import dev.langchain4j.service.AiServices;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.util.Arrays;

@SpringBootTest
public class ChatMemoryTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void test5() {
        /**
         * 你好！很高兴认识你，木芒果。这个名字听起来很有趣也很有特色。有什么我可以帮助你的吗？或者你想聊些什么呢？
         * 你刚刚告诉我，你是木芒果。如果你是在以“木芒果”作为你的昵称或代号，那么我就可以称呼你为木芒果。如果你有其他想要了解的身份信息或者有其他问题需要解答，请告诉我！
         *
         * 你好，张三！很高兴见到你。有什么我可以帮助你的吗？如果你有任何问题或需要什么信息，请随时告诉我。
         * 你刚才告诉我你是张三。如果你是在开玩笑或者有其他意思，请告诉我，我很乐意继续我们的对话！
         */
        String msg = separateChatAssistant.chat(1, "我是木芒果");
        System.out.println(msg);
        String msg2 = separateChatAssistant.chat(1, "我是谁");
        System.out.println(msg2);

        String msg3 = separateChatAssistant.chat(2, "我是张三");
        System.out.println(msg3);
        String msg4 = separateChatAssistant.chat(2, "我是谁");
        System.out.println(msg4);
    }
}
```



# 提示词

## 系统提示词

@SystemMessage：获取系统输入

@SystemMessage设定角色，塑造AI助手的专业身份，明确助手的能力范围

1.在SeparateChatAssistant类的chat方法上添加@SystemMessage注解

```java
package com.mmg.assistant;

import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider") //通过指定chatMemoryProvider实现聊天记忆隔离
public interface SeparateChatAssistant {

    @SystemMessage("你是一个我的好朋友，请用粤语回答问题。今天是{{current_date}}") // 系统提示词,使用占位符传递当前日期
    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```

2.测试

```java
import com.mmg.assistant.SeparateChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void testChat() {
        String msg = separateChatAssistant.chat(3, "今天几号？");
        System.out.println(msg);
    }
}
```

## 从资源中加载提示词模板

1.在resources目录下新建一个my-prompt-template.txt文件

```
你是一个我的好朋友，请用东北话回答问题。
今天是{{current_date}}
```

2.在@SystemMessage注解中添加fromResource属性指定提示词模板文件

```java
package com.mmg.assistant;

import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider") //通过指定chatMemoryProvider实现聊天记忆隔离
public interface SeparateChatAssistant {

//    @SystemMessage("你是一个我的好朋友，请用粤语回答问题。今天是{{current_date}}") // 系统提示词,使用占位符传递当前日期
    @SystemMessage(fromResource = "my-prompt-template.txt") // 系统提示词,引用外部提示词模板文件
    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```

3.测试

```java
import com.mmg.assistant.SeparateChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void testChat() {
        String msg = separateChatAssistant.chat(3, "今天几号？");
        System.out.println(msg);
    }
}
```

## 用户提示词模板

@UserMessage：获取用户输入

1.在MemoryChatAssistant类的chat方法上添加@UserMessage注解

```java
package com.mmg.assistant;

import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.spring.AiService;

import static dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT;


@AiService(wiringMode = EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemory = "chatMemory")
public interface MemoryChatAssistant {

    @UserMessage("你是一个我的好朋友，请用东北话回答问题。{{it}}") //通过{{it}}占位符传入用户输入
    String chat(String userMessage);
}
```

2.测试

```java
import com.mmg.assistant.MemoryChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private MemoryChatAssistant memoryChatAssistant;

    @Test
    public void testChat2() {
        String msg1 = memoryChatAssistant.chat("我是木芒果");
        System.out.println(msg1);

        String msg2 = memoryChatAssistant.chat("我今年18岁");
        System.out.println(msg2);
    }
}
```

## 使用@V注解

### 单个参数的情况

1.在MemoryChatAssistant类的chat方法上添加@UserMessage注解，使用@V注解注解自定义占位符参数

```java
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.V;
import dev.langchain4j.service.spring.AiService;

import static dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT;


@AiService(wiringMode = EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemory = "chatMemory")
public interface MemoryChatAssistant {

    @UserMessage("你是一个我的好朋友，请用东北话回答问题。{{message}}") //通过{{message}}占位符传入用户输入
    String chat(@V("message") String userMessage);
}
```

2.测试

```java
import com.mmg.assistant.MemoryChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private MemoryChatAssistant memoryChatAssistant;

    @Test
    public void testChat2() {
        String msg1 = memoryChatAssistant.chat("我是木芒果");
        System.out.println(msg1);

        String msg2 = memoryChatAssistant.chat("我今年18岁");
        System.out.println(msg2);
    }
}
```

### 多个参数的情况

1.在SeparateChatAssistant类的chat方法上添加@UserMessage注解，并使用@V注解指定用户输入参数名称

```java
import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.V;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider") //通过指定chatMemoryProvider实现聊天记忆隔离
public interface SeparateChatAssistant {

    @UserMessage("你是一个我的好朋友，请用东北话回答问题。{{message}}") // 通过{{message}}占位符传入用户输入
    String chat2(@MemoryId int memoryId, @V("message") String userMessage);
}
```

2.测试

```java
import com.mmg.assistant.SeparateChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void testChat3() {
        String msg1 = separateChatAssistant.chat2(4, "我是木芒果");
        System.out.println(msg1);

        String msg2 = separateChatAssistant.chat2(4, "我今年18岁");
        System.out.println(msg2);
    }
}
```

### @SystemMessage和@V组合使用

1.在SeparateChatAssistant类的chat方法上添加@SystemMessage注解，并使用@V注解指定用户输入参数名称

```java
package com.mmg.assistant;

import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.V;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider") //通过指定chatMemoryProvider实现聊天记忆隔离
public interface SeparateChatAssistant {

    @SystemMessage(fromResource = "my-prompt-template3.txt")
    String chat3(@MemoryId int memoryId,
                 @UserMessage String userMessage,
                 @V("username") String username,
                 @V("age") int age);
}
```

2.在resources目录下创建my-prompt-template3.txt文件

```
你是一个我的好朋友,我是{{username}},我今年{{age}}，请用东北话回答问题。
今天是{{current_date}}
```

3.测试

```java
package com.mmg;

import com.mmg.assistant.SeparateChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void testChat3() {
        String msg = separateChatAssistant.chat3(5, "我是谁？今年多大？我的出生日期是多少？", "木芒果", 18);
        System.out.println(msg);
    }
}
```



# Function Calling函数调用

Function Calling函数调用也叫Tools工具

例如，大语言模型本身并不擅长数学运算。如果应用场景中偶尔会涉及到数学计算，我们可以为他提供一个“数学工具”。当我们提出问题时，大语言模型会
判断是否使用某个工具。

## 入门

1.创建CalculatorTools类，并在方法中加上@Tool注解

```java
import dev.langchain4j.agent.tool.Tool;
import org.springframework.stereotype.Component;

@Component
public class CalculatorTools {

    @Tool
    public String sum(int a, int b) {
        System.out.println("加法工具被调用");
        return String.valueOf(a + b);
    }

    @Tool
    public double squareRoot(double x) {
        System.out.println("算术平方根工具被调用");
        return Math.sqrt(x);
    }
}
```

2.在AiServicez注解中配置tools属性

```java
package com.mmg.assistant;

import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.V;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider", //通过指定chatMemoryProvider实现聊天记忆隔离
        tools = "calculatorTools") //通过指定tools实现Function calling
public interface SeparateChatAssistant {
    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```

3.测试

```java
import com.mmg.assistant.SeparateChatAssistant;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class PromptTest {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Test
    public void testChat4() {
        String msg = separateChatAssistant.chat(6, "1+2等于几？475695037565的平方根是多少？");
        System.out.println(msg);
    }
}
```



## @Tool注解

可以通过name指定工具名称以及通过value指定工具的描述信息，让大模型更好的理解这个工具的作用

```java
package com.mmg.tools;

import dev.langchain4j.agent.tool.P;
import dev.langchain4j.agent.tool.Tool;
import org.springframework.stereotype.Component;

@Component
public class CalculatorTools {

    @Tool(name = "加法运算", value = "将两个参数a和b相加并返回运算结果") // 指定工具名称和描述
    public double sum(double a,double b) {
        System.out.println("加法工具被调用");
        return a + b;
    }

    @Tool(name = "平方根运算", value = "计算给定参数的平方根并返回结果")
    public double squareRoot(double x) {
        System.out.println("算术平方根工具被调用");
        return Math.sqrt(x);
    }
}
```



## @P注解

@P注解用来指定工具参数的名称以及是否必填

```java
package com.mmg.tools;

import dev.langchain4j.agent.tool.P;
import dev.langchain4j.agent.tool.Tool;
import org.springframework.stereotype.Component;

@Component
public class CalculatorTools {

    @Tool(name = "加法运算", value = "将两个参数a和b相加并返回运算结果") // 指定工具名称和描述
    public double sum(@P(value = "加数1", required = true) double a, @P(value = "加数2", required = true) double b) {
        System.out.println("加法工具被调用");
        return a + b;
    }

    @Tool(name = "平方根运算", value = "计算给定参数的平方根并返回结果")
    public double squareRoot(double x) {
        System.out.println("算术平方根工具被调用");
        return Math.sqrt(x);
    }
}
```



## @ToolMemoryId注解

如果你的AIService方法中有一个参数使用@MemoryId注解，那么你也可以使用@ToolMemoryId注解@Tool方法中的一个参数。提供给AIService方法的值
将自动传递给@Too1方法。如果你有多个用户，或每个用户有多个聊天记忆，并且希望在@Too1方法中对它们进行区分，那么这个功能会很有用。

```java
import dev.langchain4j.agent.tool.P;
import dev.langchain4j.agent.tool.Tool;
import dev.langchain4j.agent.tool.ToolMemoryId;
import org.springframework.stereotype.Component;

@Component
public class CalculatorTools {

    @Tool(name = "加法运算", value = "将两个参数a和b相加并返回运算结果") // 指定工具名称和描述
    public double sum(@ToolMemoryId int memoryId, @P(value = "加数1", required = true) double a, @P(value = "加数2", required = true) double b) {
        System.out.println("加法工具被调用:" + memoryId);
        return a + b;
    }

    @Tool(name = "平方根运算", value = "计算给定参数的平方根并返回结果")
    public double squareRoot(double x) {
        System.out.println("算术平方根工具被调用");
        return Math.sqrt(x);
    }
}
```





# 检索增强生成RAG

## 介绍

如何让大模型回答专业领域的知识？

LLM的知识仅限于它所训练的数据。如果你想让LLM了解特定领域的知识或专有数据，你可以：

- 使用 RAG
- 使用你的数据微调LLM
- 结合RAG和微调

微调大模型：

在现有大模型的基础上，使用小规模的特定任务数据进行再次训练，调整模型参数，让模型更精确地处理特定领域或任务的数据。更新需重新训练，计算资

源和时间成本高。

- 优点：一次会话只需一次模型调用，速度快，在特定任务上性能更高，准确性也更高。
- 缺点：知识更新不及时，模型训成本高、训练周期长。
- 应用场景：适合知识库稳定、对生成内容准确性和风格要求高的场景，如对上下文理解和语言生成质量要求高的文学创作、专业文档生成等。

RAG：

Retrieval-Augmented Generation 检索增强生成

将原始问题以及提示词信息发送给大语言模型之前，先通过外部知识库检索相关信息，然后将检索结果和原始问题一起发送给大模型，大模型依据外部知识

库再结合自身的训练数据，组织自然语言回答问题。通过这种方式，大语言模型可以获取到特定领域的相关信息，并能够利用这些信息进行回复。

- 优点：数据存储在外部知识库，可以实时更新，不依赖对模型自身的训练，成本更低。
- 缺点：需要两次查询：先查询知识库，然后再查询大模型，性能不如微调大模型
- 应用场景：适用于知识库规模大且频繁更新的场景，如企业客服、实时新闻查询、法律和医疗领域的最新知识问答等。

RAG常用方法

- 全文（关键词）搜索。这种方法通过将问题和提示词中的关键词与知识库文档数据库进行匹配来搜索文档。根据这些关键词在每个文档中的出现频率和相关性对搜索结果进行排序。
- 向量搜索，也被称为“语义搜索”文本通过嵌入模型被转换为数字向量。然后，它根据查询向量与文档向量之间的余弦相似度或其他相似性/距离度量来查找和排序文档，从而捕捉更深层次的语义含义。
- 混合搜索。结合多种搜索方法(例如，全文搜索+向量搜索）通常可以提高搜索的效果。



## 文档加载器

常见文档加载器

- 来自langchain4j模块的文件系统文档加载器(FileSystemDocumentLoader)
- 来自langchain4j 模块的类路径文档加载器(ClassPathDocumentLoader)
- 来自langchain4j 模块的网址文档加载器(UrlDocumentLoader)
- 来自langchain4j-document-loader-amazon-s3模块的亚马逊 S3 文档加载器(AmazonS3DocumentLoader)
- 来自langchain4j-document-loader-azure-storage-blob模块的 Azure Blob 存储文档加载器(AzureBlobStorageDocumentLoader)
- 来自 langchain4j-document-loader-github模块的 GitHub 文档加载器(GitHubDocumentLoader)
- 来自langchain4j-document-loader-google-cloud-storage模块的谷歌云存储文档加载器(GoogleCloudStorageDocumentLoader)
- 来自 langchain4j-document-loader-selenium模块的 Selenium 文档加载器(SeleniumDocumentLoader)
- 来自langchain4j-document-loader-tencent-cos模块的腾讯云对象存储文档加载器(TencentCosDocumentLoader)

测试FileSystemDocumentLoader

```java
package com.mmg;

import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.loader.FileSystemDocumentLoader;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class RAGTest {

    @Test
    public void test() {
        //使用FileSystemDocumentLoader读取指定目录下的知识库文档
        //并使用默认的文档解析器TextDocumentParser对文档进行解析
        Document document = FileSystemDocumentLoader.loadDocument("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\src\\main\\resources\\测试.txt");
        System.out.println(document.text());
    }
}
```

其他加载文档的方式

```java
import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.loader.FileSystemDocumentLoader;
import dev.langchain4j.data.document.parser.TextDocumentParser;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.nio.file.FileSystems;
import java.nio.file.PathMatcher;
import java.util.List;

@SpringBootTest
public class RAGTest {

    @Test
    public void test() {
        // 使用FileSystemDocumentLoader读取指定目录下的知识库文档
        // 并使用默认的文档解析器TextDocumentParser对文档进行解析
        // Document document = FileSystemDocumentLoader.loadDocument("E:\Desktop\Java\LangChain4J\java-ai-langchain4j\knowledge\测试.txt");
        // System.out.println(document.text());

        // 加载单个文档
        // Document document = FileSystemDocumentLoader.loadDocument("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge\\测试.txt", new TextDocumentParser());

        // 从一个目录中加载所有文档
        // List<Document> documents = FileSystemDocumentLoader.loadDocuments("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge", new TextDocumentParser());

        // 从一个目录中加载所有的.txt文档
        PathMatcher pathMatcher = FileSystems.getDefault().getPathMatcher("glob:*.md");
        List<Document> documents1 = FileSystemDocumentLoader.loadDocuments("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge", pathMatcher, new TextDocumentParser());
        documents1.forEach(item -> {
            System.out.println("-----------------");
            System.out.println(item.metadata());
            System.out.println(item.text());
        });


        // 从一个目录及其子目录中加载所有文档
        // List<Document> documents2 = FileSystemDocumentLoader.loadDocumentsRecursively("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge", new TextDocumentParser());

    }
}
```



## 文档解析器

文档可以是各种格式的文件，比如 PDF、DOC、TXT 等等。为了解析这些不同格式的文件，有一个 “文档解析器”（DocumentParser）接口，并且我们的库中包含了该接口的几种实现方式：

- 来自 langchain4j 模块的文本文档解析器（TextDocumentParser），它能够解析纯文本格式的文件 （例如 TXT、HTML、MD 等）。 

- 来自 langchain4j-document-parser-apache-pdfbox 模块的 Apache PDFBox 文档解析器 （ApachePdfBoxDocumentParser），它可以解析 PDF 文件。 

- 来自 langchain4j-document-parser-apache-poi 模块的 Apache POI 文档解析器 （ApachePoiDocumentParser），它能够解析微软办公软件的文件格式（例如 DOC、DOCX、PPT、 PPTX、XLS、XLSX 等）。 

- 来自 langchain4j-document-parser-apache-tika 模块的 Apache Tika 文档解析器 （ApacheTikaDocumentParser），它可以自动检测并解析几乎所有现有的文件格式。

假设如果我们想解析PDF文档，那么原有的TextDocumentParser就无法工作了，我们需要引入 langchain4j-document-parser-apache-pdfbox。

1.引入依赖

```xml
<!--解析pdf文档-->
<dependency>
	<groupId>dev.langchain4j</groupId>
	<artifactId>langchain4j-document-parser-apache-pdfbox</artifactId>
</dependency>
```

2.测试解析pdf文档

```java
import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.loader.FileSystemDocumentLoader;
import dev.langchain4j.data.document.parser.TextDocumentParser;
import dev.langchain4j.data.document.parser.apache.pdfbox.ApachePdfBoxDocumentParser;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.nio.file.FileSystems;
import java.nio.file.PathMatcher;
import java.util.List;

@SpringBootTest
public class RAGTest {
    /**
     * 解析PDF
     */
    @Test
    public void testParsePDF() {
        Document document = FileSystemDocumentLoader.loadDocument(
                "E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge\\医院信息.pdf",
                new ApachePdfBoxDocumentParser()
        );
        System.out.println(document);
    }
}
```



## 文档分割器

常见文档分割器 

LangChain4j 有一个 “文档分割器”（DocumentSplitter）接口，并且提供了几种开箱即用的实现方式： 

- 按段落文档分割器（DocumentByParagraphSplitter） 

- 按行文档分割器（DocumentByLineSplitter） 

- 按句子文档分割器（DocumentBySentenceSplitter） 

- 按单词文档分割器（DocumentByWordSplitter） 

- 按字符文档分割器（DocumentByCharacterSplitter） 

- 按正则表达式文档分割器（DocumentByRegexSplitter） 

- 递归分割：DocumentSplitters.recursive(...) 

默认情况下每个文本片段最多不能超过300个token



## 测试向量转换和向量存储

Embedding (Vector) Stores 常见的意思是 “嵌入（向量）存储” 。在机器学习和自然语言处理领域， Embedding 指的是将数据（如文本、图像等）转换为低维稠密向量表示的过程，这些向量能够保留数据 的关键特征。而 Stores 表示存储，即用于存储这些嵌入向量的系统或工具。它们可以高效地存储和检索 向量数据，支持向量相似性搜索，在文本检索、推荐系统、图像识别等任务中发挥着重要作用。

Langchain4j支持的向量存储： https://docs.langchain4j.dev/integrations/embedding-stores/

1.引入依赖

```xml
<!--简单的rag实现-->
<dependency>
	<groupId>dev.langchain4j</groupId>
	<artifactId>langchain4j-easy-rag</artifactId>
</dependency>
```

2.测试

```java
import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.loader.FileSystemDocumentLoader;
import dev.langchain4j.data.document.parser.TextDocumentParser;
import dev.langchain4j.data.document.parser.apache.pdfbox.ApachePdfBoxDocumentParser;
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.store.embedding.EmbeddingStoreIngestor;
import dev.langchain4j.store.embedding.inmemory.InMemoryEmbeddingStore;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.nio.file.FileSystems;
import java.nio.file.PathMatcher;
import java.util.List;

@SpringBootTest
public class RAGTest {

    @Test
    public void testReadDocumentAndStore() {
        //使用FileSystemDocumentLoader读取指定目录下的知识库文档
        //并使用默认的文档解析器对文档进行解析(TextDocumentParser)
        Document document = FileSystemDocumentLoader.loadDocument("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge\\人工智能.md");
        //为了简单起见，我们暂时使用基于内存的向量存储
        InMemoryEmbeddingStore<TextSegment> embeddingStore = new InMemoryEmbeddingStore<>();
        //ingest
        //1、分割文档：默认使用递归分割器，将文档分割为多个文本片段，每个片段包含不超过 300个token，并且有 30个token的重叠部分保证连贯性
        //DocumentByParagraphSplitter(DocumentByLineSplitter(DocumentBySentenceSplitter(DocumentByWordSplitter)))
        //2、文本向量化：使用一个LangChain4j内置的轻量化向量模型对每个文本片段进行向量化
        //3、将原始文本和向量存储到向量数据库中(InMemoryEmbeddingStore)
        EmbeddingStoreIngestor.ingest(document, embeddingStore);
        //查看向量数据库内容
        System.out.println(embeddingStore);
    }

}
```



## 测试文档分割

```java
import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.loader.FileSystemDocumentLoader;
import dev.langchain4j.data.document.parser.TextDocumentParser;
import dev.langchain4j.data.document.parser.apache.pdfbox.ApachePdfBoxDocumentParser;
import dev.langchain4j.data.document.splitter.DocumentByParagraphSplitter;
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.model.embedding.onnx.HuggingFaceTokenizer;
import dev.langchain4j.store.embedding.EmbeddingStoreIngestor;
import dev.langchain4j.store.embedding.inmemory.InMemoryEmbeddingStore;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.nio.file.FileSystems;
import java.nio.file.PathMatcher;
import java.util.List;

@SpringBootTest
public class RAGTest {


    /**
     * 文档分割
     */
    @Test
    public void testDocumentSplitter() {
        //使用FileSystemDocumentLoader读取指定目录下的知识库文档
        //并使用默认的文档解析器对文档进行解析(TextDocumentParser)
        Document document = FileSystemDocumentLoader.loadDocument("E:\\Desktop\\Java\\LangChain4J\\java-ai-langchain4j\\knowledge\\人工智能.md");
        //为了简单起见，我们暂时使用基于内存的向量存储
        InMemoryEmbeddingStore<TextSegment> embeddingStore = new InMemoryEmbeddingStore<>();
        //自定义文档分割器
        //按段落分割文档：每个片段包含不超过 300个token，并且有 30个token的重叠部分保证连贯性
        //注意：当段落长度总和小于设定的最大长度时，就不会有重叠的必要。
        DocumentByParagraphSplitter documentSplitter = new DocumentByParagraphSplitter(
                300,
                30,
                //token分词器：按token计算
                new HuggingFaceTokenizer());

        //按字符计算
        //DocumentByParagraphSplitter documentSplitter = new DocumentByParagraphSplitter(300, 30);

        EmbeddingStoreIngestor
                .builder()
                .embeddingStore(embeddingStore)
                .documentSplitter(documentSplitter)
                .build()
                .ingest(document);
    }

}
```



## Token和Token计算

DeepSeek：https://api-docs.deepseek.com/zh-cn/quick_start/token_usage

DeepSeek API Docs 阿里百炼：https://bailian.console.aliyun.com/?tab=model#/model-market/detail/deepseek-v3

LangChain4j：

```java
package com.mmg;

import dev.langchain4j.community.model.dashscope.QwenTokenizer;
import dev.langchain4j.data.document.Document;
import dev.langchain4j.data.document.loader.FileSystemDocumentLoader;
import dev.langchain4j.data.document.parser.TextDocumentParser;
import dev.langchain4j.data.document.parser.apache.pdfbox.ApachePdfBoxDocumentParser;
import dev.langchain4j.data.document.splitter.DocumentByParagraphSplitter;
import dev.langchain4j.data.message.UserMessage;
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.model.embedding.onnx.HuggingFaceTokenizer;
import dev.langchain4j.store.embedding.EmbeddingStoreIngestor;
import dev.langchain4j.store.embedding.inmemory.InMemoryEmbeddingStore;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.nio.file.FileSystems;
import java.nio.file.PathMatcher;
import java.util.List;

@SpringBootTest
public class RAGTest {

    @Test
    public void testTokenCount() {
        String text = "这是一个示例文本，用于测试 token 长度的计算。";
        UserMessage userMessage = UserMessage.userMessage(text);
        //计算 token 长度
        QwenTokenizer tokenizer = new QwenTokenizer(System.getenv("ALIYUN_PLATFORM_API_KEY"), "qwen-max");
        //HuggingFaceTokenizer tokenizer = new HuggingFaceTokenizer();
        int count = tokenizer.estimateTokenCountInMessage(userMessage);
        System.out.println("token长度：" + count);
    }

}
```



## 实战

1.添加依赖

```xml
<!--简单的rag实现-->
<dependency>
	<groupId>dev.langchain4j</groupId>
	<artifactId>langchain4j-easy-rag</artifactId>
</dependency>
```

2.在SeparateChatAssistantConfig中注册ContentRetriever

```java
package com.mmg.config;

import com.mmg.store.MongoChatMemoryStore;
import dev.langchain4j.memory.chat.ChatMemoryProvider;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import jakarta.annotation.Resource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SeparateChatAssistantConfig {

    @Resource
    private MongoChatMemoryStore mongoChatMemoryStore;

    @Bean
    public ChatMemoryProvider chatMemoryProvider() {
        return memoryId -> MessageWindowChatMemory.builder()
                .id(memoryId)
                .maxMessages(10)
                // 使用MongoDB作为存储
                .chatMemoryStore(mongoChatMemoryStore)
                .build();
    }
    
    @Bean
    public ContentRetriever contentRetriever() {
        // 使用ClassPathDocumentLoader读取指定目录下的知识库文档
        // 并使用默认的文档解析器对文档进行解析
        Document document1 = ClassPathDocumentLoader.loadDocument("knowledge/医院信息.md");
        Document document2 = ClassPathDocumentLoader.loadDocument("knowledge/科室信息.md");
        Document document3 = ClassPathDocumentLoader.loadDocument("knowledge/神经内科.md");
        List<Document> documents = Arrays.asList(document1, document2, document3);
        // 使用内存向量存储
        InMemoryEmbeddingStore<TextSegment> embeddingStore = new InMemoryEmbeddingStore<>();
        // 使用默认的文档分割器
        EmbeddingStoreIngestor.ingest(documents, embeddingStore);
        // 从嵌入存储（EmbeddingStore）里检索和查询内容相关的信息
        return EmbeddingStoreContentRetriever.from(embeddingStore);
    }
}
```

3.在@AiService注解中添加contentRetriever属性并指定检索增强类

```java
package com.mmg.assistant;

import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.V;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider", //通过指定chatMemoryProvider实现聊天记忆隔离
        contentRetriever = "contentRetriever") //通过contentRetriever指定检索增强
public interface SeparateChatAssistant {
    
    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```



# 向量模型和向量存储

## 向量大模型

通用文本向量模型： https://help.aliyun.com/zh/model-studio/text-embedding-synchronous-api

text-embedding-v3：https://bailian.console.aliyun.com/?tab=model#/model-market/detail/text-embedding-v3

使用通用文本向量text-embedding-v3，维度1024，维度越多，对事务的描述越精准，信息检索的精度越高。

使用 text-embedding-v3依然需要添加langchain4j-community-dashscope依赖

```xml
        <!-- 引入阿里云百炼平台所需的依赖 -->
        <dependency>
            <groupId>dev.langchain4j</groupId>
            <artifactId>langchain4j-community-dashscope-spring-boot-starter</artifactId>
        </dependency>
```

配置向量模型

```properties
#集成阿里通义千问-通用文本向量-v3
langchain4j.community.dashscope.embedding-model.api-key=${ALIYUN_PLATFORM_API_KEY}
langchain4j.community.dashscope.embedding-model.model-name=text-embedding-v3
```

文本向量化

```java
import dev.langchain4j.data.embedding.Embedding;
import dev.langchain4j.model.embedding.EmbeddingModel;
import dev.langchain4j.model.output.Response;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class EmbeddingTest {

    @Resource
    private EmbeddingModel embeddingModel;

    @Test
    public void testEmbeddingModel() {
        Response<Embedding> embed = embeddingModel.embed("你好");
        System.out.println("向量维度：" + embed.content().vector().length);
        System.out.println("向量输出：" + embed.toString());
    }
}
```



## 向量存储

默认使用的是InMemoryEmbeddingStore作为向量存储，但是不建议在生产中使用基于内存的向量存储。因此这里我们使用Pinecone作为向量数据库。

官方网站：https://www.pinecone.io/

访问官方网站、注册、登录、获取apiKey且配置在环境变量中。默认有2GB的免费存储空间。

得分的含义：

在向量检索场景中，当我们把查询文本转换为向量后，会在嵌入存储（ EmbeddingStore ）里查找与之 最相似的向量（这些向量对应着文档片段等内容）。为了衡量查询向量和存储向量之间的相似程度，会 使用某种相似度计算方法（例如余弦相似度等）来得出一个数值，这个数值就是得分。得分越高，表明 查询向量和存储向量越相似，对应的文档片段与查询文本的相关性也就越高。

得分的作用：

- 筛选结果：通过设置 minScore 阈值，能够过滤掉那些与查询文本相关性较低的结果。在代码 里， minScore(0.8) 意味着只有得分大于等于 0.8 的结果才会被返回，低于这个阈值的结果会被 舍弃。这样可以确保返回的结果是与查询文本高度相关的，提升检索结果的质量。

- 控制召回率和准确率：调整 minScore 的值可以在召回率和准确率之间进行权衡。如果把阈值设 置得较低，那么更多的结果会被返回，召回率会提高，但可能会包含一些相关性不太强的结果，导 致准确率下降；反之，如果把阈值设置得较高，返回的结果数量会减少，准确率会提高，但可能会 遗漏一些相关的结果，使得召回率降低。在实际应用中，需要根据具体的业务需求来合理设置 minScore 的值。

示例说明

假设我们有一个关于水果的文档集合，嵌入存储中存储了这些文档片段的向量。当我们使用 “苹果的营养 价值” 作为查询文本时，向量检索会计算查询向量与存储向量的相似度得分。如果 minScore 设置为 0.8，那么只有那些与 “苹果的营养价值” 相关性非常高的文档片段才会被返回，而一些只简单提及苹果但 没有详细讨论其营养价值的文档片段可能由于得分低于 0.8 而不会被返回。

### 集成Pinecone

1.引入依赖

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-pinecone</artifactId>
</dependency>
```

2.创建向量存储对象

```java
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.model.embedding.EmbeddingModel;
import dev.langchain4j.store.embedding.EmbeddingStore;
import dev.langchain4j.store.embedding.pinecone.PineconeEmbeddingStore;
import dev.langchain4j.store.embedding.pinecone.PineconeServerlessIndexConfig;
import jakarta.annotation.Resource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class EmbeddingStoreConfig {

    @Resource
    private EmbeddingModel embeddingModel;

    @Bean
    public EmbeddingStore<TextSegment> embeddingStore() {
        //创建向量存储
        EmbeddingStore<TextSegment> embeddingStore = PineconeEmbeddingStore.builder()
                .apiKey(System.getenv("PINECONE_API_KEY"))
                .index("xiaozhi-index")//如果指定的索引不存在，将创建一个新的索引
                .nameSpace("xiaozhi-namespace") //如果指定的名称空间不存在，将创建一个新的名称 空间
                .createIndex(PineconeServerlessIndexConfig.builder()
                        .cloud("AWS") //指定索引部署在 AWS 云服务上。
                        .region("us-east-1") //指定索引所在的 AWS 区域为 us-east-1。
                        .dimension(embeddingModel.dimension()) //指定索引的向量维度，该维度与embeddedModel生成的向量维度相同。
                        .build())
                .build();
        return embeddingStore;
    }
}
```

3.在SeparateChatAssistantConfig新增Pincone的配置

```java
import com.mmg.store.MongoChatMemoryStore;
import dev.langchain4j.memory.chat.ChatMemoryProvider;
import dev.langchain4j.memory.chat.MessageWindowChatMemory;
import jakarta.annotation.Resource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SeparateChatAssistantConfig {

    @Resource
    private MongoChatMemoryStore mongoChatMemoryStore;

    @Bean
    public ChatMemoryProvider chatMemoryProvider() {
        return memoryId -> MessageWindowChatMemory.builder()
                .id(memoryId)
                .maxMessages(10)
                // 使用MongoDB作为存储
                .chatMemoryStore(mongoChatMemoryStore)
                .build();
    }
    
    @Bean
    public ContentRetriever contentRetriever() {
        // 使用ClassPathDocumentLoader读取指定目录下的知识库文档
        // 并使用默认的文档解析器对文档进行解析
        Document document1 = ClassPathDocumentLoader.loadDocument("knowledge/医院信息.md");
        Document document2 = ClassPathDocumentLoader.loadDocument("knowledge/科室信息.md");
        Document document3 = ClassPathDocumentLoader.loadDocument("knowledge/神经内科.md");
        List<Document> documents = Arrays.asList(document1, document2, document3);
        // 使用内存向量存储
        InMemoryEmbeddingStore<TextSegment> embeddingStore = new InMemoryEmbeddingStore<>();
        // 使用默认的文档分割器
        EmbeddingStoreIngestor.ingest(documents, embeddingStore);
        // 从嵌入存储（EmbeddingStore）里检索和查询内容相关的信息
        return EmbeddingStoreContentRetriever.from(embeddingStore);
    }
    
    @Bean
    public ContentRetriever contentRetrieverPincone() {
        // 创建一个 EmbeddingStoreContentRetriever 对象，用于从嵌入存储中检索内容
        return EmbeddingStoreContentRetriever
                .builder()
                // 设置用于生成嵌入向量的嵌入模型
                .embeddingModel(embeddingModel)
                // 指定要使用的嵌入存储
                .embeddingStore(embeddingStore)
                // 设置最大检索结果数量，这里表示最多返回 1 条匹配结果
                .maxResults(1)
                // 设置最小得分阈值，只有得分大于等于 0.8 的结果才会被返回
                .minScore(0.8)
                // 构建最终的 EmbeddingStoreContentRetriever 实例
                .build();
    }
}
```

4.在@AiService注解中添加contentRetriever属性并指定检索增强类

```java
package com.mmg.assistant;

import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.V;
import dev.langchain4j.service.spring.AiService;

@AiService(wiringMode = dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT,
        chatModel = "qwenChatModel",
        chatMemoryProvider = "chatMemoryProvider", //通过指定chatMemoryProvider实现聊天记忆隔离
        contentRetriever = "contentRetrieverPincone") //通过contentRetriever指定检索增强
public interface SeparateChatAssistant {
    
    String chat(@MemoryId int memoryId, @UserMessage String userMessage);
}
```

5.测试新增,将内容手动插入到Pinecone中

```java
import dev.langchain4j.data.embedding.Embedding;
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.model.embedding.EmbeddingModel;
import dev.langchain4j.model.output.Response;
import dev.langchain4j.store.embedding.EmbeddingStore;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class EmbeddingTest {

    @Resource
    private EmbeddingStore embeddingStore;

    /**
     * 将文本转换成向量，然后存储到pinecone中
     * 参考：https://docs.langchain4j.dev/tutorials/embedding-stores
     */
    @Test
    public void testPineconeEmbeded() {
        //将文本转换成向量
        TextSegment segment1 = TextSegment.from("我喜欢羽毛球");
        Embedding embedding1 = embeddingModel.embed(segment1).content();
        //存入向量数据库
        embeddingStore.add(embedding1, segment1);

        TextSegment segment2 = TextSegment.from("今天天气很好");
        Embedding embedding2 = embeddingModel.embed(segment2).content();
        embeddingStore.add(embedding2, segment2);
    }

}
```



## 相似度匹配

接收请求获取问题，将问题转换为向量，在 Pinecone 向量数据库中进行相似度搜索，找到最相似的文本 片段，并将其文本内容返回给客户端。

```java
import dev.langchain4j.data.embedding.Embedding;
import dev.langchain4j.data.segment.TextSegment;
import dev.langchain4j.model.embedding.EmbeddingModel;
import dev.langchain4j.model.output.Response;
import dev.langchain4j.store.embedding.EmbeddingMatch;
import dev.langchain4j.store.embedding.EmbeddingSearchRequest;
import dev.langchain4j.store.embedding.EmbeddingSearchResult;
import dev.langchain4j.store.embedding.EmbeddingStore;
import jakarta.annotation.Resource;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class EmbeddingTest {

    @Resource
    private EmbeddingModel embeddingModel;

    /**
     * Pinecone-相似度匹配
     */
    @Test
    public void embeddingSearch() {
        //提问，并将问题转成向量数据
        Embedding queryEmbedding = embeddingModel.embed("你最喜欢的运动是什么？").content();
        //创建搜索请求对象
        EmbeddingSearchRequest searchRequest = EmbeddingSearchRequest.builder()
                .queryEmbedding(queryEmbedding)
                .maxResults(1) //匹配最相似的一条记录
                //.minScore(0.8)
                .build();
        //根据搜索请求 searchRequest 在向量存储中进行相似度搜索
        EmbeddingSearchResult<TextSegment> searchResult = embeddingStore.search(searchRequest);
        //searchResult.matches()：获取搜索结果中的匹配项列表。
        //.get(0)：从匹配项列表中获取第一个匹配项
        EmbeddingMatch<TextSegment> embeddingMatch = searchResult.matches().get(0);
        //获取匹配项的相似度得分
        System.out.println(embeddingMatch.score()); // 0.8144288515898701
        //返回文本结果
        System.out.println(embeddingMatch.embedded().text());
    }

}
```



# 流式输出

大模型的流式输出是指大模型在生成文本或其他类型的数据时，不是等到整个生成过程完成后再一次性返回所有内容，而是生成一部分就立即发送一部分给用户或下游系统，以逐步、逐块的方式返回结果。 这样，用户就不需要等待整个文本生成完成再看到结果。通过这种方式可以改善用户体验，因为用户不 需要等待太长时间，几乎可以立即开始阅读响应。

1.引入依赖

```xml
<!--流式输出-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-reactor</artifactId>
</dependency>
```

2.在application.properties中配置qwen流式输出大模型

```properties
#集成阿里通义千问-流式输出
langchain4j.community.dashscope.streaming-chat-model.api-key=${ALIYUN_PLATFORM_API_KEY}
langchain4j.community.dashscope.streaming-chat-model.model-name=qwen-plus
```

3.修改SeparateChatAssistant中chatModel改为 streamingChatModel = "qwenStreamingChatModel"以及将chat方法的返回值为Flux

```java
import dev.langchain4j.service.MemoryId;
import dev.langchain4j.service.SystemMessage;
import dev.langchain4j.service.UserMessage;
import dev.langchain4j.service.spring.AiService;
import reactor.core.publisher.Flux;

import static dev.langchain4j.service.spring.AiServiceWiringMode.EXPLICIT;

@AiService(
        wiringMode = EXPLICIT,
        streamingChatModel = "qwenStreamingChatModel", //指定qwen流式输出的模型
        chatMemoryProvider = "chatMemoryProvider",
        contentRetriever = "contentRetrieverPincone")
public interface SeparateChatAssistant {

    Flux<String> chat(@MemoryId Long memoryId, @UserMessage String userMessage);
}
```

4.在controller中指定请求的返回方式为流式输出，并且将返回类型也改为Flux

```java
import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.tags.Tag;
import jakarta.annotation.Resource;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Flux;

@Tag(name = "我的助手", description = "我的助手")
@RestController
@RequestMapping("/test")
public class TestController {

    @Resource
    private SeparateChatAssistant separateChatAssistant;

    @Operation(summary = "对话")
    @PostMapping(value = "/chat", produces = "text/stream;charset=utf-8")
    public Flux<String> chat(@RequestBody ChatForm chatForm) {
        return separateChatAssistant.chat(chatForm.getMemoryId(), chatForm.getMessage());
    }
}
```

