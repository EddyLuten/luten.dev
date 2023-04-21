---
title: CriticalSection wrapper class
date:  2008-08-22 00:00:00 -0700
layout: single
tags: [C, Tutorial, Win32]
---

*2023 Update:* You probably don't want to use this code since there are likely some serious issues with it. But, fun fact: a major tech company reached out to me to clarify what the license for this is. So, if you want to screw yourself over and use it, let's say it's MIT licensed and call it a day.

**What:** A C++ wrapper around both WINAPI (Microsoft Windows) and PThreads (POSIX threads) functionality.

**Why:** To abstract cross platform functionality.

**Remarks:** On windows, CRITICAL_SECTION objects cannot be shared cross-process. This means that the class is tied to your application or DLL process. Comments are in Doxygen/Javadoc style.

<!--more-->

```c++
#ifdef _WIN32
#include <windows.h>
#else
#include <unistd.h>
#include <pthread.h>
#endif

/**
 * @class A wrapper-class around Critical Section functionality, WIN32 & PTHREADS.
 */
class CriticalSection
{
public:
  /**
   * @brief CriticalSection class constructor.
   */
  explicit CriticalSection(void)
  {
  #ifdef _WIN32
    if (0 == InitializeCriticalSectionAndSpinCount(&this->m_cSection, 0))
      throw("Could not create a CriticalSection");
  #else
    if (pthread_mutex_init(&this->m_cSection, NULL) != 0)
      throw("Could not create a CriticalSection");
  #endif
  }; // CriticalSection()

  /**
   * @brief CriticalSection class destructor
   */
  ~CriticalSection(void)
  {
    this->WaitForFinish(); // acquire ownership
  #ifdef _WIN32
    DeleteCriticalSection(&this->m_cSection);
  #else
    pthread_mutex_destroy(&this->m_cSection);
  #endif
  }; // ~CriticalSection()

  /**
   * @fn void WaitForFinish(void)
   * @brief Waits for the critical section to unlock.
   * This function puts the waiting thread in a waiting
   * state.
   * @see TryEnter()
   * @return void
   */
  void WaitForFinish(void)
  {
    while(!this->TryEnter())
    {
    #ifdef _WIN32
      Sleep(1); // put waiting thread to sleep for 1ms
    #else
      usleep(1000); // put waiting thread to sleep for 1ms (1000us)
    #endif
    };
  }; // WaitForFinish()

  /**
   * @fn void Enter(void)
   * @brief Wait for unlock and enter the CriticalSection object.
   * @see TryEnter()
   * @return void
   */
  void Enter(void)
  {
    this->WaitForFinish(); // acquire ownership
  #ifdef _WIN32
    EnterCriticalSection(&this->m_cSection);
  #else
    pthread_mutex_lock(&this->m_cSection);
  #endif
  }; // Enter()

  /**
   * @fn void Leave(void)
   * @brief Leaves the critical section object.
   * This function will only work if the current thread
   * holds the current lock on the CriticalSection object
   * called by Enter()
   * @see Enter()
   * @return void
   */
  void Leave(void)
  {
  #ifdef _WIN32
    LeaveCriticalSection(&this->m_cSection);
  #else
    pthread_mutex_unlock(&this->m_cSection);
  #endif
  }; // Leave()

  /**
   * @fn bool TryEnter(void)
   * @brief Attempt to enter the CriticalSection object
   * @return bool(true) on success, bool(false) if otherwise
   */
  bool TryEnter(void)
  {
    // Attempt to acquire ownership:
  #ifdef _WIN32
    return(TRUE == TryEnterCriticalSection(&this->m_cSection));
  #else
    return(0 == pthread_mutex_trylock(&this->m_cSection));
  #endif
  }; // TryEnter()

private:
#ifdef _WIN32
  CRITICAL_SECTION m_cSection; //!< internal system critical section object (windows)
#else
  pthread_mutex_t m_cSection; //!< internal system critical section object (*nix)
#endif
}; // class CriticalSection
```
